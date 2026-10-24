# Settings — Technical Documentation

The settings feature lets a logged-in Lobsters user manage their account: profile fields, password, notification preferences, mailing-list mode, display preferences, two-factor authentication (TOTP), account deactivation, and three external-service integrations (Pushover, Mastodon, GitHub).

## Code layout

- `app/controllers/settings_controller.rb` — all actions for the feature
- `app/models/mastodon_app.rb` — per-instance Mastodon OAuth app registration
- `app/views/settings/` — `index`, `twofa`, `twofa_enroll`, `twofa_verify`, `mastodon_authentication`

Every action runs behind `before_action :require_logged_in_user, :show_title_h1`, so the whole feature is unavailable to anonymous visitors.

## Routes and actions

| Verb | Path | Action |
|---|---|---|
| GET | `/settings` | `index` |
| POST | `/settings` | `update` |
| POST | `/settings/deactivate` | `deactivate` |
| GET | `/settings/2fa` | `twofa` |
| POST | `/settings/2fa_auth` | `twofa_auth` |
| GET | `/settings/2fa_enroll` | `twofa_enroll` |
| GET | `/settings/2fa_verify` | `twofa_verify` |
| POST | `/settings/2fa_update` | `twofa_update` |
| POST | `/settings/pushover_auth` | `pushover_auth` |
| GET | `/settings/pushover_callback` | `pushover_callback` |
| GET | `/settings/mastodon_authentication` | `mastodon_authentication` |
| GET | `/settings/mastodon_auth` | `mastodon_auth` |
| GET | `/settings/mastodon_callback` | `mastodon_callback` |
| POST | `/settings/mastodon_disconnect` | `mastodon_disconnect` |
| GET | `/settings/github_auth` | `github_auth` |
| GET | `/settings/github_callback` | `github_callback` |
| POST | `/settings/github_disconnect` | `github_disconnect` |

## The settings page (`index` / `update`)

`index` renders the form against `@edit_user = @user.dup` so unsaved edits never mutate the session user. `update` works on `@user.clone`, and re-renders `index` in all cases.

Permitted params (`user_params`):

```ruby
params.require(:user).permit(
  :username, :email, :password, :password_confirmation, :homepage, :about,
  :email_replies, :email_messages, :email_mentions, :inbox_mentions,
  :pushover_replies, :pushover_messages, :pushover_mentions,
  :mailing_list_mode, :show_email, :show_avatars, :show_story_previews,
  :show_submitted_story_threads, :prefers_color_scheme, :prefers_contrast
)
```

Update logic worth knowing:

- A **password change requires the current password**: the guard is `params[:user][:password].empty? || @user.authenticate(params[:current_password])`. Changing other settings with an empty new-password field does *not* require the current password.
- When a new password is supplied, `@edit_user.roll_session_token` is called and `session[:u]` is re-set afterward — i.e., changing the password invalidates every other logged-in session.
- A **username change** triggers `Username.rename!(user:, from:, to:, by:)` — this is what produces the public modlog entry ("changed own username from 'X' to 'Y'"). Note the source reads the old value from `@edit_user.changed_atributes[:username]` (sic — misspelled method name on the user model).
- Failure to authenticate the current password sets `flash[:error] = "Your current password was not entered correctly."` and skips the save.

### Form sections (from `index.html.erb`)

1. **Public Profile Information** — username (validated against `Username.username_regex_s`, change creates a modlog entry), email (with a hint if the address is on the disposable-domain blocklist via `EmailBlocklistValidation.email_on_blocklist?`), "Show Email on profile" (shown only to logged-in users), homepage, about (markdown).
2. **Security Settings** — current password, new password + confirmation, and a 2FA status indicator linking to `/settings/2fa` (green "Enabled"/Disable, or Disabled/Enroll).
3. **Comment Reply Notification Settings** — `email_replies`, `pushover_replies` (requires a Pushover subscription).
4. **Comment Mention Notification Settings** — `inbox_mentions`, `email_mentions`, `pushover_mentions`.
5. **Private Message Notification Settings** — `email_messages`, `pushover_messages`; the "Receive E-mail for ModMail" checkbox is rendered **disabled and checked** — moderator notifications are mandatory.
6. **Submitted Story Comment Settings** — `show_submitted_story_threads` (show comments on your submitted stories in `/threads`).
7. **Mailing List Settings** — `mailing_list_mode` select: `0` No e-mails, `1` All stories and comments, `2` Only stories. The page displays the user's private list address `#{shortname}-#{mailing_list_token}@#{domain}`; mail sent to it posts under the user's account, so the token must stay private. Tag filters are honored.
8. **Miscellaneous Settings** — `prefers_color_scheme` radio (system/light/dark), `prefers_contrast` radio (system/normal/high), `show_story_previews`, `show_avatars`.
9. **External Accounts** — Gravatar (avatar cached from the Gravatar for the account email; "Expire cache" posts to `/avatars/expire`), plus Pushover / GitHub / Mastodon rows that render only when the corresponding service class reports `enabled?`.
10. **Invite a New User** — renders `users/invitationform` when `@user.can_invite?`, otherwise prints `@user.disabled_invite_reason`.
11. **Deactivate Account** — see below.

## Account deactivation (`deactivate`)

Requirements enforced server-side:

- `params[:user][:i_am_sure] == "1"`, else flash error `You did not check the "I am sure" checkbox.`
- `@user.authenticate(password)`, else flash error "Given password doesn't match account."

On success: `@user.delete!`; if the optional `disown` box was checked, `InactiveUser.disown_all_by_author!(@user)` reattributes the user's stories and comments to the `inactive-user` account. A `Moderation` record is created with `moderator: nil` and action `"deactivated"` (plus `", disowning their stories and comments"` when disowning). The session is reset and the user is redirected to `/`.

Consequences documented in the view: the profile shows the account as deactivated; login is blocked but a password reset reactivates; the username stays reserved; private messages are deleted (recipients keep copies); submitted stories are kept; comments with negative scores are deleted.

## Two-factor authentication (TOTP)

Constant: `TOTP_SESSION_TIMEOUT = (60 * 15)` — 15 minutes. Every enrollment step checks `Time.now.to_i - session[:last_authed].to_i` against it and bounces back to `/settings/2fa` with "Your enrollment period timed out." when exceeded.

Flow:

1. `twofa` (GET `/settings/2fa`) — asks for the current password; the submit button reads "Disable Two-Factor Authentication" if `@user.has_2fa?`, else "Continue".
2. `twofa_auth` (POST) — on `@user.authenticate(password)`: records `session[:last_authed]`, clears any stale `session[:totp_secret]`; if 2FA is already on, calls `@user.disable_2fa!` and redirects to `/settings` ("Two-Factor Authentication has been disabled."); otherwise redirects to enroll. Wrong password → "Your password was not correct."
3. `twofa_enroll` (GET) — generates `session[:totp_secret] = ROTP::Base32.random` (if absent), builds `ROTP::TOTP.new(secret, issuer: Rails.application.name).provisioning_uri(@user.email)` and renders it as a clickable SVG QR code via `RQRCode` (white fill, black modules, module_size 5, crispEdges). The raw secret is available behind a `<details>` "Reveal Secret" toggle for manual entry.
4. `twofa_verify` (GET) — form asking for the six-digit code (`inputmode: numeric`, `pattern: [0-9]+`, `autocomplete: one-time-code`).
5. `twofa_update` (POST) — assigns the session secret to `@user.totp_secret` and checks `@user.authenticate_totp(params[:totp_code])`. On success it **nils and re-rolls the session token** ("re-roll, just in case"), saves, re-sets `session[:u]`, deletes the session secret, and flashes "Two-Factor Authentication has been enabled on your account." Invalid code → flash error and redirect back to verify.

## Pushover integration

- `pushover_auth` (POST) — guards on `Pushover.enabled?` ("This site is not configured for Pushover" otherwise). Stores `session[:pushover_rand] = SecureRandom.hex` and redirects (with `allow_other_host: true`) to `Pushover.subscription_url` with success URL `settings/pushover_callback?rand=<rand>` and failure URL `settings/`.
- `pushover_callback` (GET) — rejects a blank session rand or blank `rand` param with flash errors; a **mismatch raises** (`raise "rand param ... != ..."`), it is not handled gracefully. Saves `params[:pushover_user_key]` onto the user. The success flash differs by outcome: key present → "Your account is now setup for Pushover notifications."; blank → "no longer setup" (unsubscribing goes through the same callback).

The index view shows "Subscribe With Pushover" or "Manage Pushover Subscription" depending on whether `pushover_user_key` is present.

## Mastodon integration

`MastodonApp` (table `mastodon_apps`: `name`, `client_id`, `client_secret`, timestamps; unique index on `name`) stores one OAuth client per Mastodon instance. Validations: presence of all three fields, max length 255, case-insensitive uniqueness of `name`.

- `MastodonApp.sanitized_instance_name` accepts a hostname (`foo.social`), a URL (`https://foo.social/@user`), or a handle (`@user@foo.social`) and reduces it to the hostname: strip, `delete_prefix("https://")`, take the segment before the first `/`, then after the last `@`.
- `find_or_register` reuses an existing row or calls `register_app!`, which POSTs to `https://<name>/api/v1/apps` (client_name = site domain, scopes `read:accounts`, redirect URIs = `/settings` and the callback) via `Sponge`. Errors are added to the model for: blank response, missing client credentials, `DNSError`/`NoIPsError` ("isn't resolving to an IP, check for typos?"), `JSON::ParserError`, `OpenSSL::SSL::SSLError`, `URI::InvalidURIError`. `register_app!` raises if the app already has a `client_id`.
- `oauth_auth_url(state)` → `https://<name>/oauth/authorize?response_type=code&client_id=...&scope=read:accounts&state=...&redirect_uri=<escaped>`; `redirect_uri` is `https://<domain>/settings/mastodon_callback?instance=<name>`.
- `token_and_user_from_code(code)` exchanges the code at `/oauth/token` (grant_type `authorization_code`), then calls `/api/v1/accounts/verify_credentials` with the bearer token to learn the username; returns `[tok, username]` or `[nil, nil]`.
- `revoke_token(token)` POSTs to `/oauth/revoke`; returns true when the response is `{}` or on server timeout (Sponge returns nil).

Controller flow:

1. `mastodon_authentication` (GET) — renders a form asking for the instance name/URL (e.g. `mastodon.social`); the page explains that only the `read:accounts` scope is requested, to confirm the username.
2. `mastodon_auth` (GET) — `find_or_register`; if persisted, stores `session[:mastodon_state] = SecureRandom.hex` and redirects to the instance's authorize URL; otherwise redirects back to `/settings` with the model's error messages.
3. `mastodon_callback` (GET) — requires `code`, `state`, and `state == session[:mastodon_state]`, else "Invalid OAuth state". On success stores `mastodon_oauth_token`, `mastodon_username`, `mastodon_instance` on the user and flashes `Linked to Mastodon user @username@instance.`; on failure flashes the app errors and falls through to `mastodon_disconnect`.
4. `mastodon_disconnect` (POST) — best-effort `revoke_token` (exceptions around networking are swallowed because "indie instances often disappear"), then nils the three user fields. Flash "Your Mastodon association has been removed." only if no other flash is present (the action also tears down failed auths).

## GitHub integration

- `github_auth` (GET) — stores `session[:github_state] = SecureRandom.hex`, redirects to `Github.oauth_auth_url(state)`.
- `github_callback` (GET) — requires session state, `code`, and matching `state`, else "Invalid OAuth state"; deletes the session state; `Github.token_and_user_from_code` yields `[token, username]`, which are saved as `github_oauth_token` / `github_username` with flash "Your account has been linked to GitHub user <username>." A failed exchange falls through to disconnect.
- `github_disconnect` (POST) — calls `Github.revoke_token`; if GitHub's API errors, flashes a notice telling the user to delete the token manually at `https://github.com/settings/applications`. Clears both fields and flashes "Your GitHub association has been removed."

## Gotchas for developers

- `changed_atributes` (misspelled) is relied on in `update` for the username rename; renaming the method on `User` would silently break modlog attribution.
- `pushover_callback` raises on a rand mismatch instead of rendering an error — a tampered callback produces a 500.
- `mastodon_auth` and `github_auth`/`github_callback` are GET routes that perform state-changing redirects/writes; CSRF protection does not apply to them, the `state` nonce is the only guard.
- The "Receive E-mail for ModMail" checkbox in the view reuses `f.check_box :email_messages` with `disabled: true, checked: true`; it is cosmetic — there is no separate `modmail_messages` param in `user_params`.
- OAuth/subscription redirects all pass `allow_other_host: true` because they leave the site.
