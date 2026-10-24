# Home Feed — Operations Manual

Audience: operations staff who run, support, and troubleshoot the site's story feeds.

## 1. What this feature serves

The home-feed feature is the public face of the site: the front page (hottest stories) plus the Newest, Recent, Active, Top, tag, multi-tag, category, domain, origin, and per-user story listings, the members' personal Saved / Upvoted / Hidden lists, the tag-filter preference page, and RSS/JSON renditions of the feeds. It is on the hot path of nearly all traffic, so its caching behavior is the main thing operations needs to understand.

## 2. Caching layers (what to check when pages look stale)

| Layer | Applies to | Lifetime | Notes |
|---|---|---|---|
| Full page cache | Active, Category, Domain, Origin, Front page, Multi-tag, Newest, Newest-by-user, Recent, Single-tag, Top | Controlled by the `CACHE_PAGE` deployment setting | Only when page caching is enabled for the environment |
| Story-list fragment cache | Same public listings | 45 seconds | Skipped entirely in development, for any signed-in user, and for visitors with tag filters (cookie) |
| Front-page RSS cache | Anonymous `/rss` | 2 minutes | Cache key `rss` |
| Related-tags cache | Single-tag page sidebar | 1 day | Cache key `related_<tagname>` |

Practical implications:

- Signed-out users may see listings up to ~45 seconds old and front-page RSS up to 2 minutes old. This is by design; do not chase it as a bug.
- Signed-in users always get live queries. If a signed-in user reports staleness, the issue is elsewhere.
- If the cache store's file backend is missing a file, the code quietly falls back to a live query — a burst of such fallbacks shows up as increased database load, not as errors.
- Flushing the Rails cache clears the story list, RSS, and related-tag entries together.

## 3. Authentication and access rules

- **Public, no sign-in needed:** front page, Newest, Recent, Active, Top, tag/category/domain/origin pages, Newest-by-user, and the Filtered Tags page (anonymous filters are stored in a long-lived browser cookie).
- **Sign-in required:** Hidden, Saved, and Upvoted lists. Unauthenticated requests are redirected to login.
- **RSS tokens:** the front page, Newest, Saved, and Upvoted feeds accept a personal `token` query parameter so feed readers can fetch a user's filtered/private feed without a session. Treat these token URLs as credentials: if a user reports theirs leaked, it must be rotated on their account. Private feeds are titled "Private feed for <username>" — that string in a support screenshot confirms the token was applied.

## 4. Expected behaviors that generate support tickets

| Report | Explanation | Action |
|---|---|---|
| "Stories are missing from my feeds" | User (or their browser cookie) has tag filters set; filtered tags hide stories site-wide | Have them review the Filtered Tags page and untick the tag, then **Save Filters** |
| "My filters disappeared" | Anonymous filters live in a browser cookie; clearing cookies or switching browsers loses them | Advise signing in so filters are stored on the account |
| "Score shows `~` instead of a number" | Score display is suppressed for that story/viewer by design | No action |
| "Recent page RSS shows Newest" | Intentional: the Recent list is unstable (stories leave as they're upvoted), so its feed link points at Newest | No action |
| "Top page URL with odd period redirects" | Unrecognized interval values redirect to the one-week default (`/top/1w`) | Valid formats look like `/top/5d`, `/top/2y` |
| "Page not found on a multi-tag or category URL" | Every comma-separated name must exist; one typo 404s the whole request | Correct the tag/category list |
| "Page out of bounds" error | Page parameter was negative or absurdly large (> 2^32); the app rejects it as a routing error | Expected; usually crawler noise |
| "Last Read line missing on Newest" | The marker only appears for signed-in users with older stories on the current page; it carries to later pages otherwise | No action |

## 5. The Filtered Tags page (support walkthrough)

1. User opens **Filtered Tags**. The table lists every active tag grouped by category with: Hide checkbox, tag, description (inactive tags and hotness modifiers are annotated), story count, and how many users filter the tag.
2. User ticks/unticks **Hide** boxes and clicks **Save Filters**.
3. Success is confirmed by the flash message "Your filters have been updated." and a redirect back to the page.

Notes for staff:

- Some tags cannot be filtered by ordinary users; those rows simply have no checkbox.
- Only *active* tags are listed and accepted; a stale form submission naming an inactive tag is ignored.
- Signed-in users' filters apply to their RSS feeds only through token-bearing feed URLs; plain public feed URLs are unfiltered.

## 6. Moderator-visible extras

Moderators browsing feeds see additional controls inline: "mod edit" on each story, and Edit links on domain and origin pages. Domain/origin pages also display ban status with the banning moderator and reason — useful when a submitter asks why their source is rejected.

## 7. Monitoring and capacity notes

- The feed queries exclude each viewer's filtered tags and compute pagination ("Page N" links, roughly one page flag per request). The front page and Newest are the highest-volume endpoints; their anonymous traffic should be served almost entirely from cache. A drop in cache hit rate on keys starting `stories ` is the first thing to check if database load rises.
- The Newest page performs a small write for signed-in users on every visit (it records the last-read timestamp), so it is never fully read-only.
- A general-purpose key/value store table (keys up to 50 characters) backs supporting counters and read-through caching used on every request's traffic accounting; it is intentionally unlocked on the read path. Monitor it for growth like any other hot table.
- The "related tags" computation on tag pages is cached for a day per tag; a cold cache after a flush briefly increases query cost on popular tag pages.

## 8. Incident checklist

1. Front page errors for everyone → check the cache store and database; anonymous traffic exercises both the page cache and the 45 s fragment cache.
2. Feeds stale for signed-out users beyond ~2 minutes → page caching (`CACHE_PAGE`) may be serving old files; verify the page-cache invalidation/expiry mechanism for the deployment.
3. Feed readers failing on private feeds → confirm the token parameter is intact in the subscribed URL and the account still exists.
4. RSS output malformed → the feed is standard RSS 2.0 with a 120-minute TTL hint; validate a sample item (title, link, author "domain by/via user", categories = tags).
