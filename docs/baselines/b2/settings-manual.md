# Settings

> **Status**: ✅ Active
> **Generated**: 2026-10-24T00:00:00Z
> **Last Updated**: 2026-10-24T00:00:00Z
---

## Overview

### What It Does
This document equips operations staff to support the Settings area: the single page at **/settings** where users manage profile fields, password, notification preferences, mailing-list delivery, appearance, two-factor authentication (2FA), external integrations (Gravatar, Pushover, Mastodon, GitHub), invitations, and account deactivation.

### Why It Exists
Settings is the highest-traffic self-service surface; most "I can't…" tickets (login after password change, missing notifications, 2FA lockouts, OAuth errors) resolve to one of the flows described here.

### Key Capabilities
- Walk users through saving profile/preferences and diagnosing why a save was rejected
- Support the full 2FA enroll/disable lifecycle, including its 15-minute timeout
- Support Pushover/Mastodon/GitHub connect and disconnect, including every error banner users can hit
- Handle deactivation requests with correct expectations about what is deleted and what is kept

---

## Architecture

### High-Level Design
Operationally, the feature is one form plus three guided detours that leave the site and come back:

1. **/settings** — the form; two **Save Account Settings** buttons submit the same form.
2. **2FA detour** — `/settings/2fa` → password → QR enroll → code verify → back to /settings.
3. **OAuth detours** — Pushover / Mastodon instance / GitHub authorize screens → callback → back to /settings with a success or error banner.

### Components
| Area on /settings | Support-relevant behavior |
|-----------|-----------|
| Public Profile Information | Username renames are publicly modlogged; disposable-domain e-mails get a blocklist warning |
| Security Settings | Password change needs current password; success rotates sessions (logs out other devices) |
| Notification sections (replies / mentions / messages) | Pushover boxes need an active Pushover subscription; moderator e-mail is locked on |
| Mailing List Settings | Shows the user's private list address — it acts as a posting credential |
| Miscellaneous Settings | Color scheme, contrast, previews, avatars |
| External Accounts | Connect/Disconnect rows appear only for services the site has enabled |
| Invite a New User | Form hidden when the account can't invite; the reason is printed instead |
| Deactivate Account | Password + "I am sure" required; disown option; consequences listed on-page |

### Technology Stack
Server-rendered forms; 2FA is standard TOTP (any authenticator app); integrations use each provider's OAuth consent screen. No client-side state to clear beyond normal cookies.

---

## Model Details
What the system records that you may be asked about:

- **Username rename** — creates a public moderation-log entry "changed own username from 'X' to 'Y'". Useful to confirm a rename happened and when.
- **Deactivation** — creates a moderation-log entry "deactivated" (with ", disowning their stories and comments" when disown was ticked), recorded with no acting moderator (self-service).
- **Linked accounts** — the profile stores the Mastodon instance + username and the GitHub username while linked; disconnect clears them.
- **Pushover** — a per-user key is stored after subscription; an empty key after the callback means the user unsubscribed.

---

## Database Schema
Not needed for support work. Two facts matter: preferences persist immediately on save, and the private mailing-list address is unique per user — if it leaks, mail sent to it posts as that user.

---

## API Endpoints
Pages and flows you will direct users to:

| Method | Path | Purpose | Notes |
|--------|------|--------|-------|
| GET | `/settings` | Main settings form | Login required |
| POST | `/settings` | Save | Banner: "Successfully updated settings." |
| POST | `/settings/deactivate` | Deactivate | Needs password + "I am sure" |
| GET | `/settings/2fa` | Start 2FA enroll/disable | Password prompt |
| GET | `/settings/2fa_enroll` → `/settings/2fa_verify` | QR + code verify | 15-minute window |
| POST | `/settings/pushover_auth` → GET callback | Pushover subscribe/manage | Only when site has Pushover configured |
| GET | `/settings/mastodon_authentication` → auth → callback | Mastodon connect | Accepts hostname, URL, or @user@host |
| GET | `/settings/github_auth` → callback | GitHub connect | |
| POST | `/settings/mastodon_disconnect`, `/settings/github_disconnect` | Unlink | |

---

## Authorization

| Check | Where | Support implication |
|--------|------------|------------|
| Logged-in session | all of /settings | Anonymous users can't reach any of it |
| Current password | password change, deactivation, 2FA on/off | "Wrong password" banners mean exactly that; nothing was changed |
| "I am sure" checkbox | deactivation | Unticked → explicit error, no action taken |
| 15-minute window | 2FA enroll/verify | Timeout banner → restart the flow |
| OAuth state token | Mastodon/GitHub callbacks | "Invalid OAuth state" → stale tab/replay; restart |
| `can_invite?` | invite form | If false, the printed reason explains the restriction; no settings-side override |

---

## Configuration

### Site-level switches (affect what users see)
- **Pushover not configured** → no Pushover row; direct attempts get "This site is not configured for Pushover".
- **GitHub / Mastodon integration disabled** → the corresponding External Accounts row is absent entirely (not an account problem).

### User-level defaults
| Setting | Default |
|---------|---------|
| Mailing list mode | No e-mails |
| Color scheme / Contrast | System / System |
| Show Email on profile | Off (and only ever shown to logged-in users) |
| ModMail e-mail notifications | Always on (locked) |

---

## Usage Examples

### Standard script: user can't save settings
1. Ask whether the new-password fields were filled. If yes → they must supply the correct current password (banner: "Your current password was not entered correctly.").
2. If only preferences changed, have them clear the password fields and resubmit.
3. Confirm the success banner "Successfully updated settings."

### Standard script: 2FA enrollment
1. /settings → **Enroll** → current password → **Continue**.
2. Scan QR (or **Reveal Secret** for manual entry) → **Verify and Enable** → enter six-digit code → **Verify and Enable**.
3. Expect "Two-Factor Authentication has been enabled on your account." and a sign-out of other devices (expected).
4. Timeout banner at any point → restart; the window is 15 minutes from the password step.

### Standard script: deactivation request
1. Confirm intent and read the consequences: profile marked deactivated; login blocked but password reset reactivates; username stays reserved; private messages deleted (recipients keep copies); stories kept; negative-score comments deleted; optional disowning relists all content under "inactive-user".
2. User enters password, ticks **I am sure**, optional **Disown stories/comments**, clicks **Yes, Deactivate My Account**.
3. Verify the moderation log recorded the self-deactivation if an audit is needed.

---

## Testing
After assisting, verify outcomes the same way users see them: success banners on save; the Security section showing **Enabled** (green) for 2FA; External Accounts rows showing the linked handle with a **Disconnect** action; the deactivated account's profile page showing the deactivated state.

---

## Known Issues & Caveats

| Issue | Impact | Handling |
|-------|----------|-------------|
| Pushover callback with tampered/stale token | User sees a server error page (500), not a friendly banner | Have them redo the subscription in one sitting; escalate only if reproducible |
| ModMail checkbox locked | Users may report they "can't untick" it | By design — moderator notifications are mandatory |
| Mastodon revocation is best-effort | Disconnect succeeds locally even when the instance is unreachable/defunct | No action needed; the link is removed on our side |
| GitHub revocation can fail | Notice points user to github.com/settings/applications to delete the token manually | Relay that instruction |
| Avatar changes seem ignored | Gravatar image is cached | **Expire cache** on /settings |

---

## Performance
Nothing in this feature is queued or delayed: saves, link/unlink, and deactivation all apply synchronously on submit. "It didn't take effect" reports are therefore validation failures (look for a red banner), not processing lag — except avatars, which are cached (see above).

---

## Troubleshooting

### Issue: "Logged out on my phone after changing password"
**Symptoms:** All other devices signed out following a password change or 2FA enablement.
**Cause:** Session token rotation on credential changes.
**Solution:** Expected behavior; log in again on each device.

### Issue: Mastodon connect fails before the authorize screen
**Symptoms:** Returned to /settings with one of: "isn't resolving to an IP, check for typos?", "App registration failed, is X a Mastodon instance?", "didn't return a client_id and client_secret", "responded with non-parseable JSON", "isn't a working SSL server", "isn't a valid URL".
**Cause:** The entered hostname is wrong or the server is not a functioning Mastodon instance.
**Solution:** Correct the hostname (e.g. `mastodon.social`); any of hostname / profile URL / `@user@host` formats are accepted.

### Issue: User locked out (lost password **and** TOTP device)
**Symptoms:** Cannot log in, cannot self-disable 2FA (that path requires the password).
**Cause:** Both factors lost.
**Solution:** Out of scope for self-service — escalate to the account-recovery/moderation process.

---

## Related Features

- **authentication** — login-time 2FA prompts come from the enrollment done here; password resets reactivate deactivated accounts
- **moderation** — renames and deactivations are auditable in the moderation log
- **messages / comments / inbox-notifications** — the events governed by the notification checkboxes
- **signup-invitations** — invitation sending and its restrictions

---

**Generated:** 2026-10-24T00:00:00Z
**Last Updated:** 2026-10-24T00:00:00Z
**Status:** ✅ Active
