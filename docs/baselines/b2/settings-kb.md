# Settings

> **Status**: ✅ Active
> **Generated**: 2026-10-24T00:00:00Z
> **Last Updated**: 2026-10-24T00:00:00Z
---

## Overview

### What It Does
The Settings page is where you manage everything about your account: your public profile (username, email, homepage, about text), your password, how you want to be notified about replies, mentions and private messages, whether the site mails you new stories, how the site looks for you (color scheme, contrast, previews, avatars), two-factor authentication, connections to outside services (Gravatar, Pushover, Mastodon, GitHub), inviting new members, and — should you ever want it — deactivating your account.

### Why It Exists
Your account is yours: you should be able to change your identity details, secure your login, tune notification volume, and leave the site on your own terms without asking anyone for help.

### Key Capabilities
- Update your profile and change your password (your other logged-in devices are signed out for safety)
- Choose e-mail, inbox, and Pushover notifications per event type (replies, mentions, private messages)
- Turn on two-factor authentication by scanning a QR code with an authenticator app
- Link or unlink your Mastodon and GitHub identities; subscribe to Pushover alerts
- Receive new stories (and optionally comments) by e-mail through your private list address
- Deactivate your account, optionally disowning your stories and comments

---

## Architecture

### High-Level Design
Everything is reached from one page. From **Settings** you can branch into three short guided flows and always come back:

1. **Settings page** — edit fields, tick checkboxes, press **Save Account Settings**.
2. **Two-Factor Authentication flow** — confirm password → scan QR code → enter six-digit code.
3. **Connect flows** — approve access on Pushover, your Mastodon instance, or GitHub, then return automatically.

### Components
What you'll find on the page, top to bottom:

| Section | What it's for |
|-----------|-----------|
| Public Profile Information | Username, email, show-email option, homepage, about |
| Security Settings | Password change and the Two-Factor Auth enroll/disable link |
| Comment Reply / Mention / Private Message Notification Settings | Per-event e-mail, inbox, and Pushover choices |
| Submitted Story Comment Settings | Show comments on your submitted stories in "Your Threads" |
| Mailing List Settings | Get stories (and comments) by e-mail; shows your private list address |
| Miscellaneous Settings | Color scheme, contrast, story previews, user avatars |
| External Accounts | Gravatar cache, Pushover, GitHub, Mastodon connections |
| Invite a New User | Send an invitation (when your account is allowed to) |
| Deactivate Account | Leave the site, with clearly listed consequences |

### Technology Stack
Not something you need to think about as a user — the page is a plain web form; the two-factor codes work with any standard authenticator app (TOTP), and the external connections use each service's normal "authorize this app" screen.

---

## Model Details
In plain terms, the site keeps one record of you, and the Settings page edits that record. A few details worth knowing:

- Renaming yourself is allowed, but every rename is listed publicly in the moderation log ("changed own username from 'X' to 'Y'").
- Your avatar isn't uploaded here — it comes from the Gravatar linked to your e-mail address.
- Disposable e-mail domains aren't accepted for mail delivery; the page will warn you if yours is one.
- When you link Mastodon, the site remembers your instance and username; the site only ever asks to *read* your account name, never to post.

---

## Database Schema
Not applicable for everyday use. What matters: your preferences are saved to your account the moment you press **Save Account Settings**, and your private mailing-list address is unique to you — treat it like a password, because e-mails sent to it are posted under your name.

---

## API Endpoints
You don't need any of these directly; here are the pages you'll actually visit:

| Where | What happens |
|--------|------|
| **Settings** | The main page with every section above |
| **Settings → Two-Factor Auth → Enroll/Disable** | The 2FA flow (password → QR code → six-digit code) |
| **Settings → External Accounts → Connect** | Pushover / Mastodon / GitHub authorization, then back to Settings |
| **Settings → Deactivate Account** | The account-closure form |

---

## Authorization
- You must be logged in to see Settings at all.
- Setting a **new password** or **deactivating** requires your current password.
- Turning 2FA on or off requires your password, and enrollment must be finished within **15 minutes**.
- Changing ordinary preferences doesn't require re-entering your password.

---

## Configuration
Choices you can configure, with their starting values:

| Setting | Options | Default |
|---------|---------|---------|
| Mailing list mode | No e-mails / All stories and comments / Only stories | No e-mails |
| Color scheme | System / Light / Dark | System |
| Contrast | System / Normal / High | System |
| Show Email on profile | on/off (visible to logged-in users only) | off |
| Notification checkboxes | per event: e-mail, inbox (mentions), Pushover | — |

One exception: e-mail notifications for messages from moderators are mandatory and shown as a locked, ticked checkbox.

---

## Usage Examples

### Turning on two-factor authentication
1. Next to **Two-Factor Auth**, click **Enroll** and confirm your password.
2. Scan the QR code with your authenticator app (or reveal and type the secret manually).
3. Enter the six-digit code to verify. You'll see "Two-Factor Authentication has been enabled on your account."

### Linking Mastodon
1. Under **External Accounts**, click **Connect** next to Mastodon.
2. Enter your instance — `mastodon.social`, a profile URL, or `@you@instance` all work.
3. Approve on your instance; you return linked ("Linked to Mastodon user @you@instance.").

### Leaving the site
1. Scroll to **Deactivate Account**, read the consequences list.
2. Enter your password, tick **I am sure** (and optionally **Disown stories/comments**).
3. Click **Yes, Deactivate My Account**. You can reactivate later via a password reset.

---

## Testing
Before relying on a change, verify it took effect: after saving you should see "Successfully updated settings." at the top of the page; after 2FA enrollment the Security section shows **Enabled** in green; after connecting a service its row shows your linked account name with a **Disconnect** option.

---

## Known Issues & Caveats

| Caveat | What it means for you |
|-------|-------------|
| 2FA enrollment window | You have 15 minutes from password confirmation to finish; otherwise start over |
| Password change signs out other devices | Intentional safety behavior, not a bug |
| Moderator e-mail is mandatory | The ModMail notification checkbox cannot be unticked |
| Mailing-list address is sensitive | Anyone with your list address can post as you — keep it private |
| Deactivation is thorough | Private messages are deleted (recipients keep copies); negatively-scored comments are deleted; stories remain |

---

## Performance
Settings changes apply immediately on save. The one thing that can lag is your avatar: it's cached from Gravatar, so after changing your Gravatar picture use **Expire cache** on the Settings page.

---

## Troubleshooting

### Issue: "Your current password was not entered correctly."
**Cause:** You filled in a new password but the current password was wrong or missing.
**Solution:** Enter your current password, or clear the new-password fields if you only wanted to change preferences.

### Issue: "Your enrollment period timed out."
**Cause:** More than 15 minutes passed during 2FA setup.
**Solution:** Start again from the Two-Factor Auth page and finish in one sitting.

### Issue: "Invalid OAuth state" when connecting Mastodon or GitHub
**Cause:** The connect flow was resumed from a stale tab.
**Solution:** Start the connection again from Settings and complete it without switching tabs.

### Issue: Pushover checkboxes don't do anything
**Cause:** You haven't subscribed with Pushover yet.
**Solution:** Use **Subscribe With Pushover** under External Accounts first.

---

## Related Features

- **Filtered Tags** — stories matching your tag filters are excluded from mailing-list e-mails
- **Your Threads** — where submitted-story comments appear when that setting is on
- **Private Messages / Replies / Mentions** — the events your notification settings control
- **Invitations** — the invite form lives on the Settings page

---

**Generated:** 2026-10-24T00:00:00Z
**Last Updated:** 2026-10-24T00:00:00Z
**Status:** ✅ Active
