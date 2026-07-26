# Settings

> A comprehensive guide to managing your account settings and preferences on Lobsters.

---

## What is Settings?

The Settings page is your central hub for managing everything about your Lobsters account. From here you can update your profile, change your password, enable two-factor authentication, configure how you receive notifications, adjust display preferences, link external accounts (GitHub, Mastodon, Pushover), and deactivate your account.

---

## Key Capabilities

- Edit your public profile (username, email, homepage, bio)
- Change your password
- Enable or disable two-factor authentication (2FA) using an authenticator app
- Configure notification preferences (email and push notifications for replies, mentions, and private messages)
- Subscribe to the mailing list to receive stories and comments by email
- Toggle display preferences (color scheme, contrast, avatars, story previews)
- Link or unlink your GitHub account
- Link or unlink your Mastodon account (works with any Mastodon-compatible instance)
- Set up Pushover push notifications
- Send invitations to new users
- Deactivate your account with an option to disown your content

---

## How It Works

1. Navigate to your Settings page from the site navigation (usually by clicking your username or "Settings").
2. Update any fields you want to change. For example, edit your bio, change your email, or update your homepage URL.
3. To change your password, enter your current password along with the new one.
4. To enable 2FA, go to the Two-Factor Authentication section. You will be asked to verify your current password, then scan a QR code with your authenticator app, and finally enter a verification code to confirm.
5. Configure your notification preferences by checking or unchecking the options for email notifications on replies, mentions, and messages. You can also enable Pushover push notifications.
6. To subscribe to the mailing list, select your preferred mode: all stories and comments, stories only, or disabled.
7. Adjust display preferences such as color scheme (system, light, or dark), contrast level, whether avatars are shown, and whether story previews appear in listings.
8. Link your GitHub or Mastodon account by following the authorization flow from the Settings page. You can disconnect them at any time.
9. To deactivate your account, scroll to the bottom of Settings. You must enter your password and confirm you are sure. You can optionally check "Disown my content" to transfer all your stories and comments to a generic account.

---

## Common Questions

**Q: How do I change my email address?**
A: Go to Settings and update the email field. Your avatar (from Gravatar) may not update immediately -- use the "expire avatar cache" option to refresh it.

**Q: What notification options are available?**
A: You can receive notifications by email or Pushover for: replies to your comments, mentions of your username, and private messages. You can also control whether @-mentions appear in your inbox.

**Q: What is mailing list mode?**
A: Mailing list mode sends you an email for every new story (and optionally every comment) posted on the site. You can choose to receive all stories and comments, stories only, or disable it entirely.

**Q: How does linking my GitHub or Mastodon account work?**
A: When you link your account, you are redirected to GitHub or your Mastodon instance to authorize Lobsters. Once authorized, your username from that service is displayed on your profile. You can disconnect at any time from the Settings page.

**Q: What happens when I deactivate my account?**
A: Your account is marked as deleted. Your negative-scoring comments are removed, your messages are hidden, and your unused invitations expire. If you chose to disown your content, all your stories and comments are transferred to a generic inactive account. You can reactivate later by using the password reset flow.

**Q: Can I change my username?**
A: Yes, from the Settings page. However, you can only change it once per year, and previously used usernames are reserved for five years.

**Q: What are the color scheme options?**
A: You can choose "System" (follows your device setting), "Light," or "Dark." You can also set contrast to "System," "Normal," or "High."

---

## Tips & Best Practices

- Enable two-factor authentication for better security
- Set up email or push notifications so you do not miss replies to your comments
- Link your GitHub or Mastodon account to help the community recognize you
- If you plan to deactivate, consider whether you want to disown your content first -- this cannot be undone
- Review your notification preferences periodically to avoid notification fatigue

---

## Limitations & Important Notes

- You must verify your current password to change your password or enable/disable 2FA
- The 2FA enrollment process must be completed within 15 minutes of verifying your password
- Username changes are limited to once per year
- Deactivating your account with content disowning is irreversible for the content attribution
- Pushover notifications require a Pushover account and the Pushover app
- Mastodon linking works with any Mastodon-compatible instance, but if the instance goes offline, the connection may be lost

---

## Related Features

- [Authentication](./authentication.md) -- Login and password reset flows tied to your account credentials
- [Users](./users.md) -- Your public profile that reflects the settings you configure here
- [Signup & Invitations](./signup-invitations.md) -- The invitation form on your settings page lets you invite new users
- [Inbox & Notifications](./inbox-notifications.md) -- Notification preferences set here control what appears in your inbox
- [Messages](./messages.md) -- Message notification preferences are configured in settings
