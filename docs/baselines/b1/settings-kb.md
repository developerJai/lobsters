# Your Account Settings

Everything about your Lobsters account lives on one page: **Settings** (you must be logged in to see it). From there you can update your public profile, change your password, choose how you get notified, turn on two-factor authentication, connect outside services, and — if you ever want to — deactivate your account.

## What you can manage on the Settings page

### Public profile

- **Username** — you can rename yourself, but every rename is recorded publicly in the moderation log (e.g. "changed own username from 'oldname' to 'newname'"), so everyone can follow the trail.
- **Email** — used for notifications and for your avatar (see Gravatar below). Disposable email domains aren't accepted for mail delivery; if yours is on the blocklist you'll see a note asking you to change it.
- **Show Email on profile** — optional; even when on, your address is only visible to logged-in users.
- **Homepage** and **About** — free-form profile fields. The About section supports simple formatting.

### Password

To set a new password you must also enter your **current password** — this protects your account if someone gets access to an open session. After a successful password change, any other devices where you were logged in are signed out automatically.

### Notifications

You can decide, independently, how to hear about three kinds of events:

- **Replies to your comments** — by e-mail and/or Pushover alert.
- **Mentions of your username in comments** — in your inbox, by e-mail, and/or Pushover alert.
- **Private messages** — by e-mail and/or Pushover alert. One exception: e-mail notifications for messages from the moderation team are mandatory and can't be switched off.

Pushover alerts only work after you've subscribed with Pushover (see below).

There's also a **Submitted Story Comment** option: show comments made on stories you submitted in your "Your Threads" page.

### Mailing list mode

If you prefer reading by e-mail, you can have the site send you newly submitted stories — either stories and comments, or stories only. Items hidden by your tag filters are not sent. All list mail appears addressed to a private, personal list address shown on the page; replying or writing to that address posts under your account on the site, so **keep that address secret** — anyone who knows it could post as you.

### Appearance

- **Color Scheme** — System, Light, or Dark.
- **Contrast** — System, Normal, or High.
- **Show Story Previews** and **Show User Avatars** — toggle visual extras on or off.

## Two-factor authentication (2FA)

You can protect your account with a time-based one-time code (TOTP) from an authenticator app:

1. From Settings, follow the Two-Factor Auth **Enroll** link.
2. Confirm your current password.
3. Scan the QR code with your authenticator app (or reveal the secret and type it in manually).
4. Enter the six-digit code from the app to verify and switch 2FA on.

A few things to know:

- The enrollment session expires after **15 minutes**; if you take longer, you'll be asked to start again.
- Enabling 2FA signs out your other sessions as a safety measure.
- To turn 2FA off, go back to the same page, enter your password, and confirm — that's all it takes.

## Connected accounts

### Gravatar

Your avatar comes from the Gravatar associated with your account e-mail. If you've changed your Gravatar and the site still shows the old picture, use **Expire cache** on the Settings page.

### Pushover

If the site has Pushover support switched on, you can subscribe with one click: you're taken to Pushover, approve the subscription there, and come back automatically. Afterwards the per-event Pushover checkboxes in your notification settings take effect. You can return to Pushover any time via **Manage Pushover Subscription** — unsubscribing there also switches the alerts off here.

### Mastodon

You can link your Mastodon identity to your profile:

1. Choose **Connect** next to Mastodon, and enter your instance (a hostname like `mastodon.social`, a profile URL, or your full `@user@instance` handle — all three work).
2. Approve the request on your instance. The site only asks for permission to read your account name — nothing is ever posted on your behalf.
3. You'll come back linked, e.g. "Linked to Mastodon user @you@your.instance."

Use **Disconnect** to remove the link; the site also asks your instance to revoke its access.

### GitHub

Similarly, **Connect** next to GitHub sends you to GitHub to authorize, and your GitHub username then appears on your profile. **Disconnect** removes the link and revokes the authorization; in the rare case GitHub's revocation fails, you'll be pointed to GitHub's own applications page to remove it manually.

## Inviting a new user

The Settings page also hosts the invitation form. If your account currently isn't allowed to send invitations, the page tells you why instead of showing the form.

## Deactivating your account

At the bottom of Settings you can deactivate your account. You must enter your password and tick **I am sure**. Before you do, understand what happens:

- Your profile will show that you deactivated your account.
- You won't be able to log in — but a password reset reactivates the account if you change your mind.
- Your username stays reserved; nobody else can take it.
- Your private messages are deleted (people you corresponded with keep their copies).
- Your submitted stories are **not** deleted; comments of yours with negative scores are deleted.
- Optionally, tick **Disown stories/comments** to have all your stories and comments relisted under the generic "inactive-user" name instead of your username.

## Frequently asked questions

**Why is the site asking for my current password when I only changed my password field?**
Setting a new password always requires the current one. Other settings can be saved without it.

**I clicked the QR code step but got "Your enrollment period timed out."**
2FA enrollment must be completed within 15 minutes of confirming your password. Just start again from the 2FA page.

**My Pushover checkboxes don't seem to do anything.**
They only take effect once you've subscribed via the Pushover button under External Accounts.

**Mastodon says my instance "isn't resolving" or "isn't a Mastodon instance".**
Check the spelling of the hostname; the site registers itself with your instance on first use, and that fails if the address is wrong or the server isn't a Mastodon server.

**Can moderators' messages be muted?**
No — e-mail notifications for moderator mail are mandatory.
