# Authentication

> A comprehensive guide to logging in, two-factor authentication, and password management on Lobsters.

---

## What is Authentication?

Authentication is how you prove your identity to Lobsters. You log in with your email address or username and password. For extra security, you can enable two-factor authentication (2FA) using an authenticator app. If you forget your password, you can reset it via email.

---

## Key Capabilities

- Log in using either your email address or your username
- Two-factor authentication (2FA) using an authenticator app (TOTP)
- Password reset via a time-limited email link
- Account reactivation through the password reset flow (if you previously deleted your account)
- Automatic session management that keeps you logged in across page visits
- Banned and deleted accounts are prevented from logging in

---

## How It Works

1. Visit the login page and enter your email address or username along with your password.
2. If your credentials are correct and you do not have 2FA enabled, you are logged in and redirected to the page you were trying to visit (or the homepage).
3. If you have 2FA enabled, you are prompted to enter a six-digit code from your authenticator app.
4. Once logged in, your session persists until you log out or your session expires.
5. To reset a forgotten password, click "Forgot Password" on the login page and enter your email or username. You will receive an email with a reset link that expires after 24 hours.
6. If you previously deleted your account, completing a password reset will reactivate it.
7. To log out, click "Logout" in the site navigation. This ends your session immediately.

---

## Common Questions

**Q: Can I log in with either my email or username?**
A: Yes. The login form accepts either your email address or your username.

**Q: What is two-factor authentication (2FA)?**
A: 2FA adds an extra layer of security. After entering your password, you must also enter a six-digit code from an authenticator app (such as Google Authenticator or Authy). This means even if someone learns your password, they cannot access your account without your phone.

**Q: How do I enable or disable 2FA?**
A: Go to your Settings page. There is an option to enable 2FA, which will guide you through scanning a QR code with your authenticator app. You can disable it from the same page by entering your password.

**Q: How long does the password reset link last?**
A: The password reset link expires after 24 hours. If it expires, you will need to request a new one.

**Q: What happens if I try to log in to a banned account?**
A: You will see a message that your account has been banned, along with the reason. The system also logs this attempt for moderators to review.

**Q: Can I reactivate a deleted account?**
A: Yes. If you deleted your account (and were not banned), you can use the password reset flow to reactivate it. After setting a new password, your account becomes active again.

**Q: Why does it say my password is too long?**
A: Passwords are limited to 72 bytes for security reasons. If your password uses non-ASCII characters (which take multiple bytes each), it may exceed this limit. You will need to use the password reset flow to set a shorter password.

---

## Tips & Best Practices

- Enable two-factor authentication for better account security
- Use a unique, strong password for your Lobsters account
- If you have 2FA enabled, keep a backup of your authenticator setup in case you lose your device
- Log out when using shared or public computers

---

## Limitations & Important Notes

- Passwords cannot exceed 72 bytes in length
- Password reset links expire after 24 hours and can only be used once
- Banned users cannot reset their password or log in
- Accounts that were privacy-wiped (deleted before a previous server migration) cannot be recovered through the normal password reset flow
- Two-factor authentication requires an authenticator app that supports TOTP (Time-based One-Time Passwords)

---

## Related Features

- [Signup & Invitations](./signup-invitations.md) -- How to create a new account through the invitation system
- [Settings](./settings.md) -- Where you enable or disable 2FA and change your password
- [Users](./users.md) -- Your user profile and account information
