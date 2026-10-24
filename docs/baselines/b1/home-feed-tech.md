# Home Feed — Technical Documentation

Audience: developers working on the Lobsters codebase.

## Scope

The home-feed feature covers every public story listing on the site: the hottest front page, newest, active, recent, top-by-interval, saved/hidden/upvoted personal lists, and listings filtered by tag, category, domain, or origin. It also covers per-user tag filtering (the `/filters` page) and the RSS/JSON representations of each feed.

Implementation lives in:

- `app/controllers/home_controller.rb` — all feed actions
- `app/controllers/filters_controller.rb` — tag-filter management
- `app/controllers/concerns/story_finder.rb` — shared story lookup concern
- `app/models/keystore.rb` — generic key/value store used by supporting infrastructure
- `app/views/home/` — the shared `index.html.erb` list view, per-feed header partials, and the `stories.rss.builder` RSS template
- `app/views/filters/index.html.erb` — the filter management form

## HomeController

`HomeController` includes `IntervalHelper` and exposes fourteen feed actions. Every HTML action renders the single shared view `home/index` with per-action instance variables:

| Variable | Meaning |
|---|---|
| `@stories` | page of stories from `StoriesPaginator` |
| `@show_more` | whether a next page exists |
| `@title` | page title (empty string on the front page) |
| `@above` / `@below` | partial (or `{partial:, locals:}` hash) rendered above/below the story list |
| `@rss_link`, `@comments_rss_link` | alternate-feed link metadata |
| `@page` | validated page number, set in a `before_action` |

### Actions

- **`index`** — the front page. `Story.hottest(@user, filtered_tags.map(&:id))`. Sets Open Graph meta tags (`og:type`, `og:title`, `og:image` `touch-icon-144.png`, `og:description`). `@root_path = true`, so pagination links go to `/page/N`. RSS: for a token-identified user renders a "Private feed for #{username}"; for anonymous visitors the rendered XML is fetched through `Rails.cache` under key `"rss"` with a 2-minute expiry.
- **`newest`** — `Story.newest`. Maintains a *last read* marker: `@last_read_timestamp` comes from `params[:last_read_timestamp]` (epoch seconds) or `@user.last_read_newest_story`, then the action touches `user.last_read_newest_story`. The view inserts a `Last Read` divider before the first story older than the marker; if the marker was not shown on this page, `@next_page_params` carries `last_read_timestamp` forward so the divider can appear on a later page.
- **`newest_by_user`** — `Story.newest_by_user(@user, by_user)` where `by_user = User.find_by!(username: params[:user])` (404 on unknown username).
- **`recent`** — `Story.recent(@user, filtered_tags.map(&:id), unmerged: false)`; the newest stories that have not yet reached the front page. HTML only; its advertised RSS link deliberately points at `newest.rss` because the recent list is unstable (upvoted stories get removed).
- **`active`** — `Story.active`; "Active Discussions", stories sorted by last comment to foster active discussions (per the `_active` partial hint).
- **`top`** — parses `params[:length]` through `IntervalHelper#time_interval`. A placeholder result redirects to `top_path(length: "1w")` (HTML and RSS). Title is e.g. "Top Stories of the Past 2 Weeks" (pluralized) or "Top Stories of the Past Week" when `dur == 1`. The `_top` partial tells users they can edit the URL (`/5d`, `/2y`) and lists the known interval units from `IntervalHelper::TIME_INTERVALS`. RSS href is built manually: `"/top/#{length[:param]}/rss"`. No JSON format.
- **`single_tag`** — `Tag.find_by!(tag: params[:tag])`, stories via `Story.tagged(@user, [@tag])`. Related tags are computed by `Tag.related(@tag)` and cached one day under `"related_#{@tag.tag}"`. The header partial surfaces hotness modifier (raises/lowers a story's rank), privileged tags ("Only mods can use this tag"), tags not permitted for new users, and whether the viewer has filtered the tag.
- **`multi_tag`** — `params[:tag]` is comma-split; `raise ActiveRecord::RecordNotFound unless @tags.length == tag_params.length` (all names must resolve). Shows a note when some of the requested tags are in the viewer's filters.
- **`category`** — same comma-split + all-must-exist pattern on `Category`; stories via `Story.categories(@user, categories)`. Cache key uses the sorted, comma-joined category list.
- **`for_domain`** / **`for_origin`** — `Domain.find_by!(domain: params[:id])` / `Origin.find_by!(identifier: params[:identifier])`; stories via `@domain.stories.base(@user).order(id: :desc)` (same for origin). Header partials show story count, submitter count, origin count (domain only), ban information (banned-at, banning moderator, reason), and a mod-only Edit link.
- **`hidden`**, **`saved`**, **`upvoted`** — personal lists guarded by `require_logged_in_user`. `hidden` is HTML-only; `saved` and `upvoted` also serve RSS (titled as private feeds) and JSON. `upvoted` queries `@user.upvoted_stories.includes(:tags).order("votes.id DESC")`.

Note: `hidden` and `saved` both pass `hidden: true` as their `get_from_cache` key options — harmless in practice because logged-in requests bypass the cache entirely, but a latent key collision.

### Formats

Most actions respond to HTML, RSS (`stories.rss.builder`, rendered without layout), and JSON (`render json: @stories`). Exceptions: `recent` and `hidden` render HTML only; `top` serves HTML and RSS but not JSON.

### Filtered tags

Every main feed query receives `filtered_tags.map(&:id)` so stories carrying a filtered tag are excluded. Filters come from the user record, or from a cookie for anonymous visitors (see FiltersController).

### RSS tokens

`before_action :find_user_from_rss_token, only: [:index, :newest, :saved, :upvoted]` lets feed readers authenticate with a `token` query parameter; `user_token_link(...)` embeds it in advertised feed URLs. With a token present the feed applies the user's tag filters and titles itself "Private feed for #{username}" (newest/upvoted append " - Private feed for ..." only when `params[:token]` is present).

### Pagination

`page` reads `params[:page].to_i`; `0` becomes `1`, and negative or `> 2**32` raises `ActionController::RoutingError.new("page out of bounds")`. `paginate(scope)` wraps `StoriesPaginator.new(scope, page, @user).get`, which returns `[stories, show_more]`. The view renders "Page N-1" / "Page N+1" links (root path uses `/page/N`), merging `@next_page_params` when present.

### Caching

Two layers:

1. **Page caching** — `caches_page :active, :category, :for_domain, :for_origin, :index, :multi_tag, :newest, :newest_by_user, :recent, :single_tag, :top, if: CACHE_PAGE`.
2. **Fragment caching** — `get_from_cache(opts)` yields directly in development, for logged-in users, or when the visitor has filtered tags (users can have hidden stories; visitors can filter tags by cookie). Otherwise it builds a sorted key string of `opts.merge(page: page)` prefixed with `"stories "` and uses `Rails.cache.fetch(..., expires_in: 45)` seconds, falling back to a direct yield on `Errno::ENOENT`.

## FiltersController

`before_action :authenticate_user` (identifies the viewer; login not mandatory) and `show_title_h1`. `skip_after_action :clear_session_cookie, only: [:index]` keeps the session alive so the CSRF check succeeds on `update`.

- **`index`** — loads `Category.includes(:tags).where(tags: {active: true})` ordered by category then tag; computes `Tagging.group(:tag_id).count` (stories per tag) and `TagFilter.group(:tag_id).count` (how many users filter each tag) as two separate queries for performance; indexes the viewer's filtered tags by id.
- **`update`** — `Tag.active.where(tag: (params[:tags] || {}).keys)`, then `keep_if { |t| t.user_can_filter? @user }`. Logged-in: assigns `@user.tag_filter_tags`. Anonymous: writes `cookies.permanent[TAG_FILTER_COOKIE]` with comma-joined tag names. Flashes "Your filters have been updated." and redirects to `filters_path`.

The view is a table grouped by category: Hide checkbox (only for tags the viewer may filter), tag link, description (with `inactive` marker and non-zero `hotness mod` shown), story count, and count of users filtering that tag; submitted by a **Save Filters** button. Copy explains that anonymous filters live in a long-lasting browser cookie and that logged-in users can apply filters in feed readers via `rss_token` URLs.

## StoryFinder concern

`find_story` locates a story by `short_id` from `params[:story_id] || params[:id]`; admins may additionally look up by primary key (`Story.find(params[:id])`) as a convenience without generally permitting enumeration. For a logged-in user it hydrates `story.current_vote` from the user's story-level `Vote`. `find_story!` assigns `@story` and raises `ActiveRecord::RecordNotFound` when absent.

## Keystore model

A generic key/value table with `self.primary_key = "key"`, `MAX_KEY_LENGTH = 50`, and validations (key presence, case-insensitive uniqueness, max length; explicit `id` presence). Class API:

- `get(key)` / `value_for(key)`
- `put(key, value)` — validates key length, then `upsert`
- `increment_value_for` / `incremented_value_for(key, amount = 1)` — transactional upsert with `on_duplicate: Arel.sql("value = value + 1")`, returns the new value
- `decrement_value_for` / `decremented_value_for(key, amount = -1)` — delegate to the increment pair
- `find_or_create_key_for_update(key, init)` — pessimistic-lock loop that retries on `ActiveRecord::RecordNotUnique`
- `readthrough_cache(key, &blk)` — deliberately lock/transaction-free because `TrafficHelper` calls it on the hot path of every request
- `validate_input_key` raises `ActiveRecord::ValueTooLong` past 50 characters

Caveat: the `on_duplicate` SQL always adds 1 regardless of the `amount` argument, so `increment_value_for(key, 5)` only inserts 5 on first write; an existing row increments by 1.

## Views

`home/index.html.erb` renders `@above`, then an `<ol class="stories list">` using an inlined copy of `stories/_listdetail` (marked `heinous_inline_partial`; do not edit the copy — the source partial is canonical). Each row shows: upvote arrow with score (or `~` when `show_score_to_user?` is false; anonymous upvoters link to login), title (with `[Story removed by moderator/submitter]` for gone stories), merge badges, a `&#x2636;` description indicator, tags, domain/origin link, byline ("authored by"/"via" + user link), inline story preview (`details.story_content`) when the user enables previews, and per-user controls: edit, mod edit, suggest, flag/unflag, hide/unhide, save/unsave, archive caches (Archive.org, Ghostarchive), and the comment-count link. `hidden` adds a `show_hidden` class; `newest` injects the `Last Read` divider. The nav renders prev/next page links.

`stories.rss.builder` emits RSS 2.0 with channel title `"#{Rails.application.name}: #{@title}"`, self `atom:link`, `ttl 120`, and per-item title, link (`Routes.url_or_comments_url`), guid (short-id URL), author string `"#{domain} by|via #{username}"`, pubDate, comments URL, markeddown description (plus a Comments link for URL stories), and one `category` per tag.

## Testing

- `spec/controllers/home_controller_spec.rb`
- `spec/requests/home_spec.rb`
- `spec/models/keystore_spec.rb`

## Operational notes

- Anonymous feed pages are cached 45 s (fragment) / up to page-cache lifetime; the anonymous front-page RSS is cached 2 minutes. Stale-looking lists for logged-out users are expected within those windows.
- `top` RSS URLs are hand-built strings; changing the route requires updating the controller.
- All multi-value listing endpoints (`multi_tag`, `category`) 404 if *any* requested name is unknown.
