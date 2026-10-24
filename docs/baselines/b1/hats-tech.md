# Hats — Technical Documentation

Hats are Lobsters' verified-affiliation flair system. A hat is a short label (e.g., "OpenBSD Developer") attached to a user account that can be worn on a comment or private message to indicate the user is speaking officially for a project, organization, or company. The feature spans two models (`Hat`, `HatRequest`), two controllers (`HatsController`, `HatRequestsController`), a view helper (`HatsHelper`), and five ERB views.

## Domain model

### `Hat` (`app/models/hat.rb`)

- `belongs_to :user` — the wearer.
- `belongs_to :granted_by_user, class_name: "User", inverse_of: false` — the moderator (or system actor) who granted it.
- Includes the shared `Token` concern.
- Callbacks: `before_validation :assign_short_id, on: :create` (generates a `short_id` via `ShortId.new(self.class).generate`) and `after_create :log_moderation`.
- Validations:
  - `hat` — presence, max length 255.
  - `link` — max length 255.
  - `modlog_use` — must be `true` or `false` (inclusion validation).
  - `short_id` — presence, max length 10.
- `to_param` returns `short_id`, so all hat URLs are keyed by short id, not the numeric primary key.
- Scope `active`: `joins(:user).where(doffed_at: nil).merge(User.active)` — a hat is active only while it is undoffed **and** its wearer is an active user.

Key instance methods:

- `doff_by_user_with_reason(user, reason)` — writes a `Moderation` row with action `Doffed hat "<hat>"` and the supplied reason, then sets `doffed_at = Time.current` and saves. `moderator_user_id` is set to the acting user only when that user is a moderator; a self-doff records `nil` as the moderator.
- `log_moderation` (after_create) — writes a `Moderation` row with action `Granted hat "<hat>"`, appending ` (<link>)` when a link is present. `moderator_user_id` is the granting user; `created_at` is copied from the hat.
- `sanitized_link` — if `link` contains `@` it is treated as an email address and only the domain (via `Mail::Address#domain`) is returned; otherwise the raw link is returned. Used to avoid exposing email addresses to logged-out visitors.
- `to_txt` — plain-text rendering, `"(<hat>) "`.

### `HatRequest` (`app/models/hat_request.rb`)

- `belongs_to :user`.
- Includes `Token`.
- Validations: `hat` presence + max 255; `link` presence + max 255; `comment` presence + max 65,535.
- `attr_accessor :rejection_comment` (declared, not used elsewhere in these files).
- `approve_by_user_for_reason!(user, reason)` — in a transaction: creates a `Hat` (`user_id` = requester, `granted_by_user_id` = approving moderator, copying `hat` and `link`), sends the requester a `Message` with subject `Your hat "<hat>" has been approved` and body `reason + (" " * 20)` (the 20 trailing spaces are an explicit kludge to satisfy a minimum body length of 20 characters), then destroys the request.
- `reject_by_user_for_reason!(user, reason)` — in a transaction: sends the requester a `Message` with subject `Your request for hat "<hat>" has been rejected` and body `reason`, then destroys the request.

In both paths the request row is destroyed; the request list is therefore always a pending queue — there is no persisted approved/rejected state.

## Controllers

### `HatsController`

Filters:

- `require_logged_in_user` for everything except `index` (the hats listing is public).
- `find_hat!` for `doff`, `doff_by_user`, `edit`, `update_in_place`, `update_by_recreating`. Moderators look up any hat by `short_id` (`Hat.find_by(short_id:)`); non-moderators are restricted to `@user.wearable_hats`.
- `only_hat_user_or_moderator` for `doff`/`doff_by_user`: the hat's owner or any moderator may proceed; others are redirected to their own profile.
- `require_logged_in_moderator` for `edit`, `update_in_place`, `update_by_recreating`.

Actions:

- `index` — builds `@hat_groups`, a hash of active hats grouped by hat text (`Hat.active.includes(:user)`), rendered as a table grouped case-insensitively by hat and sorted by username.
- `doff` / `doff_by_user` — doffing form and handler. A blank `reason` is rejected with flash error "You must give a reason for the doffing." and a redirect back to the form; otherwise `doff_by_user_with_reason` runs and the user is redirected to their profile.
- `edit` / `update_in_place` — moderator edit of `hat` and `link` on the existing row. On success a `Moderation` entry is written whose action concatenates `renamed hat "<old>" to "<new>"` and/or `changed link from "<old>" to "<new>"` for whichever attributes actually changed, then redirects to the hats index. Validation failure flashes the error messages and returns to the edit form.
- `update_by_recreating` — moderator "doff & create" flow: builds a brand-new `Hat` with the new name, `doffed_at: nil`, and the original `user_id`, `granted_by_user_id`, `link`, and `modlog_use`; on save, the old hat is doffed with reason `To replace with "<new name>"`. This preserves history (the old hat remains, doffed) instead of rewriting it.

### `HatRequestsController`

Filters: `require_logged_in_user` for all actions; `require_logged_in_moderator` for `approve` and `reject` only.

- `new` / `create` — any logged-in user can request a hat by supplying `hat`, `link`, and `comment` (moderator-only justification). Success flashes "Successfully submitted hat request." and redirects to `/hats`; failure re-renders the form.
- `index` — lists all pending requests (`HatRequest.all.includes(:user)`). Note the before_action gate here is login, not moderator status, although the page's approve/reject forms post to moderator-only actions.
- `approve` — updates the request's `hat`/`link` from the submitted form (`params.require(:hat_request).permit(:hat, :link, :reason).except(:reason)` — reason is permitted then excluded from the mass update), then calls `approve_by_user_for_reason!` and flashes "Successfully approved hat request." Moderators can therefore adjust the hat text or link before approving.
- `reject` — calls `reject_by_user_for_reason!` and flashes "Successfully rejected hat request."

## Rendering (`HatsHelper`)

- `styled_hat(hat)` — renders `<span class="hat hat_<normalized>">`, where the normalization downcases the hat text and replaces every non-alphanumeric character with `_` (enabling per-hat CSS). The span's `title` tooltip is `Granted <YYYY-MM-DD>`, with ` - <sanitized_link>` appended when the link is present but not an `http(s)` URL.
- `hat_text(hat, hl)` — inner `<span class="crown">`. When the link is an `http(s)` URL the hat text becomes a hyperlink opened with `target="_blank"` and `rel="noopener"`; otherwise the hat text is plain escaped text.

## Views

- `hats/index.html.erb` — public listing under the About subnav. Explains the concept, shows a **Request Hat** link for logged-in users, and renders a zebra table (User / Hat / Link). Link cell logic: `http` links are clickable (`rel="ugc"`); blank links show "None"; non-URL links (typically emails) are shown raw to logged-in users but only as `sanitized_link` (domain) to logged-out visitors. Doffed timestamps are labelled when present, and moderators get an extra **Edit** column.
- `hats/doff.html.erb` — doffing form showing User and Hat read-only plus a **Reason** text field (hint: `Short public explanation, like "Left project"`), submitted with **Doff Hat**.
- `hats/edit.html.erb` — moderator form with **Hat** and **Link** text fields and two submit buttons targeting different actions: **Edit In-Place** (`update_in_place`) and **Doff & Create** (`update_by_recreating`).
- `hat_requests/new.html.erb` — request form (Hat, Link, Comment) with policy guidance: hats are for speaking officially, not for commemorating past work; linking a GitHub-authed account speeds verification; when you can no longer speak for the organization, contact a moderator to doff — old messages keep showing the hat, but it cannot be used again.
- `hat_requests/index.html.erb` — moderation queue. Each request shows the requester (with request age), editable required **Hat** and **Link** fields, the comment rendered as Markdown, a required **Reason** textarea, and **Approve Hat Request** / **Reject Hat Request** buttons (reject styled as a destructive action). Shows "No hat requests." when empty.

## Routes (as exercised by controllers/views)

| Path helper | Action | Access |
|---|---|---|
| `hats_path` (`/hats`) | `hats#index` | public |
| `doff_hat_path(hat)` | `hats#doff` | hat owner or moderator |
| `doff_by_user_hat_path(hat)` (POST) | `hats#doff_by_user` | hat owner or moderator |
| `edit_hat_path(hat)` | `hats#edit` | moderator |
| `update_in_place_hat_path(hat)` (POST) | `hats#update_in_place` | moderator |
| `update_by_recreating_hat_path(hat)` (POST) | `hats#update_by_recreating` | moderator |
| `new_hat_request_path` | `hat_requests#new` | logged-in user |
| `hat_requests_path` (GET/POST) | `hat_requests#index` / `#create` | logged-in user |
| `approve_hat_request_path(hr)` (POST) | `hat_requests#approve` | moderator |
| `reject_hat_request_path(hr)` (POST) | `hat_requests#reject` | moderator |

## Caveats for developers

- `HatRequestsController#index` is gated on login only; any logged-in user can view the pending request queue (approve/reject remain moderator-only).
- `find_hat!` uses `find_by`, so a missing/foreign `short_id` yields `@hat = nil` and the subsequent `@hat.user` in `only_hat_user_or_moderator` raises `NoMethodError` rather than returning 404.
- The approval message body appends 20 spaces to the reason — a deliberate kludge around `Message` body length validation.
- `modlog_use` is preserved by `update_by_recreating` but is not exposed in the moderator edit form; hats created through request approval never set it explicitly.
- Approval and rejection destroy the `HatRequest`, so no request history survives beyond the moderation log and the notification message.
