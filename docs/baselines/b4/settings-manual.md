# Settings — User Manual

> Step-by-step instructions for using Settings.

---

## Prerequisites

- You must be logged in — the Settings page is only available to signed-in users
- Have your current password ready for sensitive actions: changing your password, turning two-factor authentication on or off, and deactivating your account
- For two-factor authentication: an authenticator app installed on your device
- For external connections: an account on the relevant service (Pushover, Mastodon, or GitHub); these options only appear if the site has the integration enabled

---

## Overview

This guide covers every task on the **Settings** page: editing your profile and preferences, changing your password, setting up two-factor authentication, choosing notifications, receiving stories by e-mail, connecting outside accounts, inviting a new user, and deactivating your account. Everything lives on a single page; changes are saved with the **Save Account Settings** button (it appears twice on the page — both save the same form) and confirmed with the message "Successfully updated settings."

---

## Task 1: Edit Your Profile

### Steps

1. Open **Settings**
2. Update any of the profile fields:
   - **Username** — your public name; note that renames are recorded publicly in the moderation log (e.g. "changed own username from 'X' to 'Y'")
   - **E-mail** — avoid disposable e-mail addresses; the form warns you, and such domains don't receive site e-mail
   - **Show e-mail** — optional toggle for displaying your address
   - **Homepage** and **About** — optional profile content
3. Click **Save Account Settings**

### Expected Result

The page confirms with "Successfully updated settings." and your profile reflects the changes.

---

## Task 2: Change Your Password

### Steps

1. Open **Settings**
2. Enter your **current password**
3. Enter the new password in the **New Password** field (and its confirmation)
4. Click **Save Account Settings**

### Expected Result

"Successfully updated settings." appears, and you are signed out on every other device — this is intentional protection in case someone else had access to your account. If you only meant to change other settings and are asked for your password, check whether your browser autofilled the New Password field; clear both password fields and save again.

---

## Task 3: Turn On Two-Factor Authentication

### Steps

1. From **Settings**, start two-factor enrollment
2. Confirm your **current password**
3. Scan the QR code with your authenticator app — or use the reveal-secret option and type the secret into the app manually (keep a safe copy of this secret as a backup)
4. Enter the six-digit code from your app and press **Verify and Enable**

### Expected Result

Two-factor authentication is active; your codes will be checked at login. You have **15 minutes** from confirming your password to finish — taking longer shows "Your enrollment period timed out." and you must start again. An incorrect code shows "Your TOTP code was invalid…"; check the current code in your app and retry.

To turn two-factor authentication off later, return to the same place and confirm with your password.

---

## Task 4: Choose Your Notifications

### Steps

1. Open **Settings**
2. For each activity type — comment replies, mentions, and private messages — choose how you want to be notified: by e-mail, in your inbox, or as a Pushover push alert
3. Click **Save Account Settings**

### Expected Result

Notifications follow your choices. Two notes: the e-mail notification for messages from moderators is always on (its checkbox is ticked and locked), and Pushover alerts only work after you have subscribed to Pushover (Task 6).

---

## Task 5: Receive Stories by E-mail (Mailing-List Mode)

### Steps

1. Open **Settings** and find the mailing-list option
2. Choose your delivery mode: all stories and comments, or only stories
3. Click **Save Account Settings**

### Expected Result

The site delivers content to a private personal e-mail address associated with your account. Stories you've filtered by tag are excluded from delivery.

---

## Task 6: Subscribe to Pushover

### Steps

1. Open **Settings**, section **External Accounts**
2. Choose the Pushover option
3. Approve the subscription on Pushover's site; you return to Settings automatically
4. Now select which Pushover alerts you want in your notification settings (Task 4) and save

### Expected Result

Push alerts arrive for the activity types you selected.

---

## Task 7: Connect Your Mastodon Account

### Steps

1. Open **Settings**, section **External Accounts**, and choose to connect Mastodon
2. In the **Name or URL** box, enter your instance — a hostname like `mastodon.social`, a full URL, or your `@you@instance` handle all work
3. Approve the request on your instance — the site asks only for read access to your account identity

### Expected Result

Your Mastodon account appears linked on your profile. To unlink later, use the disconnect option; the site also asks your instance to cancel the authorization (if the instance no longer exists, the link is still removed on this side).

---

## Task 8: Connect Your GitHub Account

### Steps

1. Open **Settings**, section **External Accounts**, and choose to connect GitHub
2. Approve the authorization on GitHub

### Expected Result

Your GitHub account appears linked on your profile. To unlink, use the disconnect option. If GitHub's side fails to cancel the authorization, you'll see a notice asking you to remove it manually in your GitHub application settings.

---

## Task 9: Invite a New User

### Steps

1. Open **Settings** and find the invitation form
2. Fill it in and send the invitation

### Expected Result

The invitation is sent. If your account isn't currently allowed to invite, the page shows the reason instead of the form.

---

## Task 10: Deactivate Your Account

### Steps

1. Open **Settings** and go to the deactivation section
2. Enter your **password**
3. Tick the **"I am sure"** checkbox
4. Optionally tick the **disown** option if you want your stories and comments relisted under the generic "inactive-user" name
5. Confirm the deactivation

### Expected Result

Your account stops working immediately. Your username stays reserved for you and your submitted stories remain on the site (under your name, or under "inactive-user" if you disowned them). The deactivation is recorded in the public moderation log. You can reactivate later by performing a password reset.

---

## Variations

### Refreshing Your Avatar

Your avatar comes from the Gravatar service for your e-mail address. After changing your picture at Gravatar:

1. Open **Settings**, section **External Accounts**
2. Use **Expire cache** next to the Gravatar entry

Your new picture appears once the cached copy is refreshed.

### Appearance Preferences

In the same settings form you can adjust the site's color scheme, contrast, story previews, and user avatars. Tick or select your preferences and click **Save Account Settings** as with any other change.

---

## Settings & Configuration

Navigate to **Settings**

| Setting | Description | Notes |
|---------|-------------|---------|
| Mailing-list mode | All stories and comments, or only stories, by e-mail | Tag-filtered stories excluded |
| Notification choices | E-mail / inbox / Pushover per activity type | Moderator e-mail is locked on |
| Color scheme & contrast | Site appearance | — |
| Story previews & avatars | Show or hide visual extras | — |
| Show e-mail | Display your address on your profile | Optional |

---

## Troubleshooting

### Saving unexpectedly asks for your password

**Cause:** Your browser autofilled the New Password field, turning the save into a password change.
**Solution:** Clear both password fields and save again, or enter your current password if you do want to change it.

### "Your enrollment period timed out." during two-factor setup

**Cause:** More than 15 minutes passed after confirming your password.
**Solution:** Start the enrollment again and complete it in one sitting with your authenticator app ready.

### "Your TOTP code was invalid…"

**Cause:** The code had rotated by the time you submitted it.
**Solution:** Check the current code in your authenticator app and try again.

### "Invalid OAuth state" when connecting Mastodon or GitHub

**Cause:** The approval returned from a stale tab or an interrupted session.
**Solution:** Go back to Settings and run the connect flow again from start to finish in one browser session.

### Mastodon: "isn't resolving to an IP, check for typos?" or "is X a Mastodon instance?"

**Cause:** The instance name doesn't exist as typed, or the server at that address isn't a working Mastodon instance.
**Solution:** Re-enter the instance — hostname, full URL, or `@you@instance` handle are all accepted.

### Pushover alerts never arrive

**Cause:** The Pushover subscription hasn't been completed.
**Solution:** Subscribe via the Pushover option under External Accounts first, then select the alerts you want and save.

### Signed out on other devices after a security change

**Cause:** Password changes and two-factor enablement renew your session everywhere.
**Solution:** This is intentional; simply log in again on each device.
