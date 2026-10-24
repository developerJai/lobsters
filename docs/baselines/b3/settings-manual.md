# Settings — User Manual

> Step-by-step instructions for using Settings.

---

## Prerequisites

- You must be logged in to your account — the Settings page is not available to visitors
- For password changes, account deactivation, and two-factor authentication you'll need your current password
- For Pushover alerts, a (free) Pushover account; for Mastodon/GitHub linking, an account on that service
- Some rows under External Accounts (Pushover, GitHub, Mastodon) appear only when the site has that integration enabled

---

## Overview

This guide walks you through every task on the **Settings** page: updating your profile and preferences, changing your password, enabling and disabling two-factor authentication, connecting external accounts, receiving stories by e-mail, inviting a new user, and deactivating your account. The page's subnav also links to your **Public Profile**, your **Filtered Tags**, and **Logout**.

---

## Task 1: Update Your Profile and Preferences

### Steps

1. Navigate to **Settings**
2. In **Public Profile Information**, fill in:
   - **Username** — your public name; note each rename is recorded in the public moderation log
   - **Email** — used for notifications and your Gravatar; disposable e-mail domains are warned against
   - **Show Email on profile** — optional; shown only to logged-in users
   - **Homepage** — optional link on your profile
   - **About** — free text with simple formatting
3. Adjust any other sections (notifications, mailing list, appearance — see below)
4. Click **Save Account Settings**

### Expected Result

The page reloads with the message "Successfully updated settings."

---

## Task 2: Change Your Password

### Steps

1. Navigate to **Settings**, section **Security Settings**
2. Enter your **Current Password**
3. Enter the **New Password** and repeat it under **Confirm Password**
4. Click **Save Account Settings**

### Expected Result

"Successfully updated settings." appears — and you are signed out on all other devices (a safety measure). If you see "Your current password was not entered correctly.", re-enter the current password; nothing was changed.

---

## Task 3: Enable Two-Factor Authentication

### Steps

1. Navigate to **Settings**, section **Security Settings**; next to **Two-Factor Auth** click **Enroll**
2. Enter your **Current Password** and click **Continue**
3. Scan the QR code with your authenticator (TOTP) app — or expand **Reveal Secret** and type the secret into the app manually
4. Click **Verify and Enable**
5. Enter the six-digit **TOTP Code** from your app and click **Verify and Enable**

### Expected Result

"Two-Factor Authentication has been enabled on your account." The Security section now shows **Enabled** in green. Other devices are signed out. Note: you have **15 minutes** from step 2 to finish; after that you'll see "Your enrollment period timed out." and must restart.

---

## Task 4: Disable Two-Factor Authentication

### Steps

1. Next to **Two-Factor Auth** (showing **Enabled**), click **Disable**
2. Enter your **Current Password**
3. Click **Disable Two-Factor Authentication**

### Expected Result

"Two-Factor Authentication has been disabled." and the setting shows Disabled again.

---

## Task 5: Set Up Notifications

### Steps

1. On **Settings**, work through the three notification sections:
   - **Comment Reply Notification Settings** — tick **Receive E-mail** and/or **Receive Pushover Alert**
   - **Comment Mention Notification Settings** — tick **Show in Inbox**, **Receive E-mail**, and/or **Receive Pushover Alert**
   - **Private Message Notification Settings** — tick **Receive E-mail** and/or **Receive Pushover Alert** (e-mail for moderator messages is always on and cannot be unticked)
2. Optionally, under **Submitted Story Comment Settings**, tick **Show in Your Threads**
3. Click **Save Account Settings**

### Expected Result

Notifications follow your choices from now on. Pushover options only work after Task 6.

---

## Task 6: Subscribe With Pushover

### Steps

1. Under **External Accounts**, click **Subscribe With Pushover**
2. Approve the subscription on the Pushover site
3. You are returned to Settings automatically

### Expected Result

"Your account is now setup for Pushover notifications." The button label changes to **Manage Pushover Subscription**. To stop alerts, use that button and unsubscribe at Pushover — you'll then see "Your account is no longer setup for Pushover notifications."

---

## Task 7: Connect Mastodon

### Steps

1. Under **External Accounts**, click **Connect** next to **Mastodon**
2. In **Name or URL**, enter your instance — e.g. `mastodon.social`, a profile URL, or `@you@instance` — and click **Continue**
3. Approve the authorization on your instance (only read access to your account name is requested)

### Expected Result

Back on Settings: "Linked to Mastodon user @you@your.instance." Your profile now shows the linked handle. To unlink later, click **Disconnect** — "Your Mastodon association has been removed."

---

## Task 8: Connect GitHub

### Steps

1. Under **External Accounts**, click **Connect** next to **GitHub**
2. Authorize the application on GitHub

### Expected Result

"Your account has been linked to GitHub user <name>." To unlink, click **Disconnect**; you'll see "Your GitHub association has been removed." (If GitHub reports an error revoking the token, follow the on-screen note to delete it at GitHub's applications settings page.)

---

## Task 9: Deactivate Your Account

### Steps

1. Scroll to **Deactivate Account** and read the consequences listed on the page
2. Enter your password under **Verify Password**
3. Tick **I am sure** (required); optionally tick **Disown stories/comments**
4. Click **Yes, Deactivate My Account**

### Expected Result

You are logged out and returned to the homepage with a goodbye message. Your profile shows the account as deactivated; your username stays reserved; private messages are deleted (recipients keep copies); stories remain; negatively-scored comments are deleted. If you disowned, all your stories and comments are relisted under "inactive-user". You can reactivate later by resetting your password.

---

## Variations

### Receiving Stories by E-mail (Mailing List Mode)

Use this if you prefer reading by e-mail instead of visiting the site.

1. Under **Mailing List Settings**, set **Receive List E-mails** to **All stories and comments** or **Only stories**
2. Click **Save Account Settings**
3. Note your personal **List Address** shown in the section — keep it secret; e-mails you send to it are posted under your account. Stories matching your tag filters are not mailed.

### Refreshing Your Avatar

Your avatar is cached from the Gravatar for your e-mail address. After changing your Gravatar, click **Expire cache** next to **Gravatar** under External Accounts.

### Inviting a New User

Under **Invite a New User**, fill in the invitation form and send. If your account isn't currently allowed to invite, the page shows the reason instead of the form.

---

## Settings & Configuration

### Miscellaneous Settings

Navigate to **Settings > Miscellaneous Settings**

| Setting | Description | Default |
|---------|-------------|---------|
| Color Scheme | System / Light / Dark page appearance | System |
| Contrast | System / Normal / High | System |
| Show Story Previews | Show preview text under story titles | On |
| Show User Avatars | Show avatars next to usernames | On |

### Mailing List Settings

| Setting | Description | Default |
|---------|-------------|---------|
| Receive List E-mails | No e-mails / All stories and comments / Only stories | No e-mails |
| List Address | Your private posting/delivery address (read-only) | — |

---

## Troubleshooting

### "Your current password was not entered correctly." when saving

**Cause:** Something was typed (possibly autofilled by your browser) in the New Password field, which makes the current password mandatory.
**Solution:** Enter your current password — or clear the New Password and Confirm Password fields if you didn't mean to change it — and save again.

### "Your enrollment period timed out." during 2FA setup

**Cause:** More than 15 minutes passed since you confirmed your password.
**Solution:** Go back to **Settings > Two-Factor Auth**, re-enter your password, and complete the QR scan and code entry within 15 minutes.

### "Your TOTP code was invalid…"

**Cause:** The code expired (they rotate every 30 seconds) or your device clock is off.
**Solution:** Wait for a fresh code and retry; check your phone's automatic time setting.

### "Invalid OAuth state" when connecting Mastodon or GitHub

**Cause:** The connection was completed from a stale tab or interrupted session.
**Solution:** Return to **Settings** and start the **Connect** flow again, finishing it in the same tab.

### Mastodon: "isn't resolving to an IP, check for typos?" (or "is X a Mastodon instance?")

**Cause:** The instance name is misspelled, or the server isn't a working Mastodon instance.
**Solution:** Re-enter the instance hostname carefully (e.g. `mastodon.social`) and continue.

### Pushover checkboxes have no effect

**Cause:** No active Pushover subscription on your account.
**Solution:** Complete Task 6 (**Subscribe With Pushover**) first, then tick the Pushover checkboxes and save.
