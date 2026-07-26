# Authentication -- User Manual

> Step-by-step instructions for logging in, logging out, using two-factor authentication, and resetting your password.

---

## Prerequisites

- A registered Lobsters account
- For two-factor authentication: a TOTP-compatible authenticator app (such as Google Authenticator, Authy, or similar)

---

## Overview

Lobsters uses email/username and password authentication with optional TOTP-based two-factor authentication. You can log in using either your email address or username. If you forget your password, you can reset it via email. Deleted accounts can be reactivated through the password reset flow.

---

## Task 1: Log In

### Steps

1. Click **Login** in the site header (or navigate to the login page).
2. Enter your email address or username in the **E-mail or Username** field.
3. Enter your password in the **Password** field.
4. Click **Login**.

### Expected Result

You are redirected to the home page (or to the page you were trying to access before being prompted to log in). Your username appears in the site header.

---

## Task 2: Log In with Two-Factor Authentication

### Steps

1. Follow steps 1-4 from Task 1.
2. After entering your password, you are redirected to the two-factor authentication page.
3. Open your authenticator app and find the Lobsters entry.
4. Enter the current 6-digit code in the **TOTP Code** field.
5. Click **Login**.

### Expected Result

You are logged in and redirected to the home page. The TOTP code is valid for one interval (typically 30 seconds) with a small drift tolerance.

---

## Task 3: Log Out

### Steps

1. Click **Logout** in the site header.
2. Confirm when prompted: "Are you sure you want to logout?"

### Expected Result

Your session is destroyed and you are redirected to the home page as an anonymous visitor.

---

## Task 4: Reset a Forgotten Password

### Steps

1. Navigate to the login page.
2. Click **Reset your password** below the login form.
3. Enter your email address or username in the **E-mail or Username** field.
4. Click **Reset Password**.
5. Check your email for a password reset message.
6. Click the reset link in the email (valid for 24 hours).
7. Enter your new password in the **New Password** field.
8. Enter it again in the **Confirm Password** field.
9. Click **Submit** to set your new password.

### Expected Result

Your password is updated. If you do not have two-factor authentication enabled, you are automatically logged in. If you do have two-factor authentication, you are redirected to the login page to sign in with your new password.

---

## Task 5: Reactivate a Deleted Account

### Steps

1. Follow the same steps as Task 4 (Reset a Forgotten Password).
2. When you complete the password reset, your account is automatically reactivated.

### Expected Result

Your account is restored to active status. A moderation log entry records the reactivation. You are logged in automatically (or redirected to the login page if you have two-factor authentication).

---

## Variations

### Logging In from a Specific Page

If you try to access a page that requires login (such as submitting a story), you are redirected to the login page. After logging in, you are automatically taken back to the page you were trying to access.

---

## Troubleshooting

### "Invalid e-mail address and/or password" with a correct password

**Cause:** Your password may exceed 72 bytes (the maximum for the password hashing algorithm). Non-ASCII characters use multiple bytes per character, so a long password with special characters may exceed this limit.
**Solution:** Use the **Reset your password** flow to set a shorter password.

### "Your account has been banned" message

**Cause:** A moderator has banned your account. The ban reason is displayed in the error message.
**Solution:** Contact the site administrators if you believe this was done in error. The ban reason provides context for why the action was taken.

### Password reset link says "Invalid reset token"

**Cause:** The reset token expires after 24 hours, or it has already been used (tokens are single-use).
**Solution:** Request a new password reset. Make sure you click the link within 24 hours and only use it once.

### Two-factor authentication code is rejected

**Cause:** Your authenticator app's clock may be out of sync, or you entered the code after it expired.
**Solution:** Wait for a new code to appear in your authenticator app and try again. Ensure your device's clock is synchronized with an internet time server.
