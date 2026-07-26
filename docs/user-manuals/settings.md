# Settings -- User Manual

> Step-by-step instructions for managing your account settings on Lobsters.

---

## Prerequisites

- A registered Lobsters account (logged in)
- For two-factor authentication: a TOTP-compatible authenticator app
- For external accounts: accounts on GitHub, Mastodon, or Pushover (optional)

---

## Overview

The settings page is your central hub for managing your profile, security, notifications, display preferences, external account connections, invitations, and account deactivation. All changes are saved with the **Save Account Settings** button.

---

## Task 1: Edit Your Public Profile

### Steps

1. Click your username in the site header and then click **Settings** (or navigate directly to the settings page).
2. Under the **Public Profile Information** section:
   - Edit your **Username** if desired (can only be changed once per year).
   - Edit your **Email** address.
   - Check or uncheck **Show Email on profile** to control whether logged-in users see your email.
   - Enter or update your **Homepage** URL.
   - Edit your **About** bio (supports Markdown formatting).
3. Click **Save Account Settings**.

### Expected Result

A success message confirms your changes. Your public profile is updated immediately.

---

## Task 2: Change Your Password

### Steps

1. Navigate to the **Settings** page.
2. Scroll to the **Security Settings** section.
3. Enter your current password in the **Current Password** field.
4. Enter your new password in the **New Password** field.
5. Re-enter your new password in the **Confirm Password** field.
6. Click **Save Account Settings**.

### Expected Result

Your password is updated. Your session token is rotated, which logs out all other active sessions.

---

## Task 3: Enable Two-Factor Authentication

### Steps

1. Navigate to the **Settings** page.
2. In the **Security Settings** section, click **Enroll** next to **Two-Factor Auth**.
3. Enter your current password and click **Submit**.
4. You see a QR code. Open your authenticator app and scan the QR code (or manually enter the secret key shown below the QR code).
5. Click **Continue**.
6. Enter the 6-digit code from your authenticator app in the **TOTP Code** field.
7. Click **Verify**.

### Expected Result

Two-factor authentication is enabled. The status changes to **Enabled** on the settings page. You will be required to enter a TOTP code every time you log in.

---

## Task 4: Disable Two-Factor Authentication

### Steps

1. Navigate to the **Settings** page.
2. In the **Security Settings** section, click **Disable** next to **Two-Factor Auth**.
3. Enter your current password and click **Submit**.

### Expected Result

Two-factor authentication is removed from your account. You will no longer need a TOTP code to log in.

---

## Task 5: Configure Notification Preferences

### Steps

1. Navigate to the **Settings** page.
2. Under **Comment Reply Notification Settings**:
   - Check **Receive E-mail** to get email notifications for comment replies.
   - Check **Receive Pushover Alert** to get push notifications (requires Pushover subscription).
3. Under **Comment Mention Notification Settings**:
   - Check **Show in Inbox** to see @-mention notifications in your inbox.
   - Check **Receive E-mail** for email on mentions.
   - Check **Receive Pushover Alert** for push notifications on mentions.
4. Under **Private Message Notification Settings**:
   - Check **Receive E-mail** for email on private messages.
   - Check **Receive Pushover Alert** for push notifications on messages.
5. Click **Save Account Settings**.

### Expected Result

Your notification preferences are saved. You will receive notifications through the channels you selected.

---

## Task 6: Set Display Preferences

### Steps

1. Navigate to the **Settings** page.
2. Scroll to the **Miscellaneous Settings** section.
3. Under **Color Scheme**, select one of:
   - **System** (follows your operating system setting)
   - **Light**
   - **Dark**
4. Under **Contrast**, select one of:
   - **System**
   - **Normal**
   - **High**
5. Check or uncheck **Show Story Previews** to toggle story text previews in feed listings.
6. Check or uncheck **Show User Avatars** to toggle avatar display.
7. Click **Save Account Settings**.

### Expected Result

Your display preferences are saved and take effect immediately.

---

## Task 7: Connect a GitHub Account

### Steps

1. Navigate to the **Settings** page.
2. Scroll to the **External Accounts** section.
3. Click **Connect** next to **GitHub**.
4. You are redirected to GitHub to authorize the connection.
5. Click **Authorize** on GitHub.

### Expected Result

You are redirected back to your settings page. Your GitHub username appears next to the GitHub label. To disconnect, click **Disconnect**.

---

## Task 8: Connect a Mastodon Account

### Steps

1. Navigate to the **Settings** page.
2. Scroll to the **External Accounts** section.
3. Click **Connect** next to **Mastodon**.
4. Enter your Mastodon instance name (e.g., "mastodon.social") on the form that appears.
5. Click **Submit**.
6. You are redirected to your Mastodon instance to authorize the connection.
7. Click **Authorize** on your Mastodon instance.

### Expected Result

You are redirected back to your settings page. Your Mastodon handle appears next to the Mastodon label. To disconnect, click **Disconnect**.

---

## Task 9: Deactivate Your Account

### Steps

1. Navigate to the **Settings** page.
2. Scroll to the **Deactivate Account** section at the bottom.
3. Enter your current password in the **Verify Password** field.
4. Check the **I am sure** checkbox.
5. Optionally, check **Disown stories/comments** if you want all your content attributed to the "inactive-user" account.
6. Click **Yes, Deactivate My Account**.

### Expected Result

Your account is deactivated. You are logged out and redirected to the home page. Your profile shows "User deactivated own account." You can reactivate by resetting your password.

---

## Variations

### Mailing List Mode

Under **Mailing List Settings**, you can subscribe to receive all stories and comments (or stories only) via email. Select your preference from the **Receive List E-mails** dropdown and click **Save Account Settings**. Your private mailing list address is shown below the dropdown.

### Refreshing Your Avatar

Under **External Accounts**, click **Expire cache** next to **Gravatar** to refresh your avatar after changing it on Gravatar.

---

## Troubleshooting

### Two-factor enrollment times out

**Cause:** The enrollment window expires after 15 minutes. If you take longer than 15 minutes between entering your password and completing the verification, the process times out.
**Solution:** Start the enrollment process again from the settings page.

### Cannot change username

**Cause:** Usernames can only be changed once per year, and a username that was used by anyone in the last 5 years cannot be claimed.
**Solution:** Wait until the cooldown period has passed.

### Mastodon connection fails with "App registration failed"

**Cause:** The Mastodon instance may be down, not running Mastodon-compatible software, or may have DNS/SSL issues.
**Solution:** Verify the instance hostname is correct and accessible. Try again later if the instance is temporarily unavailable.
