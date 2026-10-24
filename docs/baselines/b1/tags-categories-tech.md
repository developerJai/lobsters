# Tags & Categories — Technical Documentation

Technical documentation for developers working on the Lobsters tag and category subsystem.

## Overview

Lobsters organizes stories with a two-level taxonomy: every **tag** belongs to exactly one **category**. Tags are applied to stories (via `Tagging` join records owned by the stories feature), and users can personally filter out stories carrying tags they don't want to see (via `TagFilter`). This feature covers the public tags listing page, the `Tag`, `Category`, and `TagFilter` models, and the admin-only category CRUD screens.

Tag creation/editing itself happens in the moderation area (`new_mod_tag_path` / `edit_mod_tag_path` links are rendered from the tags index for admins), but the domain models live here.

## Components

| File | Role |
|---|---|
| `app/controllers/tags_controller.rb` | Public tags index (HTML + JSON) |
| `app/controllers/categories_controller.rb` | Admin-only category new/create/edit/update |
| `app/models/tag.rb` | Tag domain model |
| `app/models/category.rb` | Category domain model |
| `app/models/tag_filter.rb` | Join model: user ⇄ tag filtering |
| `app/views/tags/index.html.erb` | Tags listing grouped by category |
| `app/views/tags/_multi_tag_tip.html.erb` | Hint partial: `/t/tag1,tag2` |
| `app/views/categories/_form.html.erb` | Shared new/edit category form |
| `app/views/categories/_multi_category_tip.html.erb` | Hint partial: `/categories/foo,bar` |
| `app/views/categories/new.html.erb`, `edit.html.erb` | Thin wrappers rendering `_form` |

## Model: `Tag`

### Associations

```ruby
belongs_to :category
has_many :taggings, dependent: :delete_all
has_many :stories, through: :taggings
has_many :tag_filters, dependent: :restrict_with_exception
has_many :filtering_users,
  class_name: "User",
  through: :tag_filters,
  source: :user,
  dependent: :delete_all
has_one :moderation, dependent: :restrict_with_exception
has_many :suggested_taggings, dependent: :restrict_with_exception
```

Note the mixed `dependent:` strategy: taggings are bulk-deleted, but a tag with tag_filters, a moderation record, or suggested taggings cannot be destroyed (`restrict_with_exception`). In practice tags are deactivated (`active: false`), not deleted.

### Validations

- `tag`: presence, max length 25, **case-sensitive** uniqueness, format `/\A[A-Za-z0-9_\-+]+\z/` (letters, digits, underscore, hyphen, plus)
- `description`: max length 100
- `hotness_mod`: must be in `-10..10` (per-tag adjustment to story hotness ranking)
- `permit_by_new_users`, `privileged`, `active`, `is_media`: must be boolean (`inclusion: {in: [true, false]}`)

### Flags (attributes)

| Flag | Meaning |
|---|---|
| `active` | Inactive tags can no longer be used on new stories; shown struck/dim on the index |
| `privileged` | Only moderators can apply or filter the tag |
| `is_media` | Media tag; gets `tag_is_media` CSS class; excluded from `related` suggestions |
| `permit_by_new_users` | When false, new users may not use the tag (`not_permitted_for_new_users` scope) |
| `hotness_mod` | Integer −10..10 ranking modifier |

### Scopes

- `active` — `where(active: true)`
- `not_permitted_for_new_users` — `where(permit_by_new_users: false)`
- `related(tag)` — the 8 most co-occurring active tags: joins taggings on stories that carry the given tag, excluding the tag itself, excluding tag id **67** (hardcoded: "programming", the catch-all), and excluding media tags, grouped and ordered by co-occurrence count descending, limit 8.

### Key methods

- `to_param` → the tag name; tags appear in URLs by name, not id.
- `Tag.all_with_filtered_counts_for(user)` — active tags ordered by name, restricted to tags `can_be_applied_by?(user)`, each populated with `filtered_count` from a single grouped `TagFilter` count query.
- `category_name` / `category_name=` — virtual attribute; the setter does `Category.find_by category:`.
- `css_class` → `"tag tag_<name>"` plus `" tag_is_media"` when media.
- `user_can_filter?(user)` — `active? && (!privileged? || user.try(:is_moderator?))`.
- `can_be_applied_by?(user)` — privileged tags require a moderator; otherwise `true`. A code comment notes tags a new user can't use are intentionally included so submission produces an explicit error.
- `filtered_count` — memoized count of `TagFilter` rows for this tag.
- `as_json` — serializes `tag`, `description`, `privileged`, `is_media`, `active`, `hotness_mod`, plus `category` (the category name). **Bug/caveat:** the `only:` list contains `:permit_by_new_user` (missing trailing `s`), which does not match the real column, so that flag is effectively absent from JSON output.

### Auditing

`after_save :log_modifications` creates a `Moderation` record on every create/update, describing either "Created new tag …" (all attributes) or "Updating tag <name>, changed <field> from 'x' to 'y'" per `saved_changes`. The acting moderator comes from the virtual `edit_user_id` (`attr_accessor`), which controllers must merge into params.

## Model: `Category`

```ruby
has_many :tags, -> { order("tag asc") }, dependent: :restrict_with_exception, inverse_of: :category
has_many :stories, through: :tags
has_one :moderation, dependent: :restrict_with_exception
```

- Validations: `category` presence, max length 25, **case-insensitive** uniqueness, format `/\A[A-Za-z0-9_-]+\z/` (note: unlike tags, `+` is not allowed).
- `to_param` → category name (URLs by name).
- Same `after_save :log_modifications` auditing pattern as `Tag`, writing `category_id` on the Moderation record and using `edit_user_id`.
- A category with tags cannot be destroyed (`restrict_with_exception`); there is no destroy action anyway.

## Model: `TagFilter`

Minimal join model: `belongs_to :tag`, `belongs_to :user`. A row means "this user filters out stories with this tag."

## Controllers & Endpoints

### `TagsController`

- `GET /tags` (`index`) — public, no authentication. Sets `@title = "Tags"`, loads categories alphabetically with tags preloaded, all tags with category preloaded, and `@filtered_tags` (the current viewer's filtered tags, indexed by id, via the shared `filtered_tags` helper).
  - `format.html` → `index` view
  - `format.json` → `render json: @tags` (array of `Tag#as_json`)

### `CategoriesController`

All actions gated by `before_action :require_logged_in_admin` — admin only.

| Action | Behavior |
|---|---|
| `new` | Builds `Category.new`, title "Create Category" |
| `create` | `Category.create!(category_params)`; on success flashes `"Category <name> has been created"` and redirects to `tags_path`. **Caveat:** because `create!` raises on invalid records, the `else` branch (error flash + redirect to `new_category_path`) is unreachable — invalid input raises `ActiveRecord::RecordInvalid` instead of rendering a friendly error. |
| `edit` | Looks up by `params[:category_name]` with `first!` (404 on unknown name) |
| `update` | Same lookup; on success flashes `"Category <name> has been updated"` and redirects to `tags_path`; on failure flashes error messages and redirects to `edit_category_path` |

`category_params` permits `:category_name` and `:category` and merges `edit_user_id: @user.id` (feeds the audit callback). Note `Category` has no `category_name=` writer — only the `:category` field is submitted by the form, so the extra permit is inert.

## Views

- `tags/index.html.erb`: intro paragraph linking to `/filters` ("You can filter out stories by tag, even if you don't have an account") and noting "Inactive tags can no longer be used on new stories." Then, per category: an `h2` linking to `category_path(category)`, an admin-only category "edit" link, and an ordered list of the category's tags showing the tag link, description (dimmed with `inactive_tag` class when the tag is inactive or filtered by the viewer), an "inactive" marker, a "filtered" link to `/filters#<tag>` when the viewer filters it, and an admin-only "edit" link (to the mod area). Admins also get "Create New Tag" (mod area) and "Create New Category" links at the bottom.
- `categories/_form.html.erb`: one required text field labelled **Name** (`autocapitalize: off`); submit label is "Create Category" or "Update Category" depending on persistence; posts to `categories_path` or `update_category_path`.
- Tip partials document multi-selection URLs: `/t/tag1,tag2` for tags, `/categories/foo,bar` for categories.

## Known Issues & Caveats

1. `Tag#as_json` typo: `:permit_by_new_user` instead of `:permit_by_new_users` — flag silently missing from the JSON API.
2. `CategoriesController#create` uses `create!`, making its error-handling branch dead code; validation failures surface as exceptions.
3. Hardcoded tag id `67` ("programming" catch-all) excluded in `Tag.related`.
4. Uniqueness is case-sensitive for tags but case-insensitive for categories; formats also differ (`+` allowed in tags only).
5. No destroy endpoints for tags or categories; `restrict_with_exception` associations make deletion unsafe by design.

## Related Features

- **stories** — owns `Tagging` and `SuggestedTagging`; stories are tagged at submission.
- **home-feed** — `/t/<tag>` and `/categories/<name>` feeds; `filters_controller` manages a user's `TagFilter` rows.
- **moderation** — tag create/edit lives under `mod/tags`; every tag/category change writes a `Moderation` log entry.
