# Settings

> A comprehensive guide to Settings.

---

## What is Settings?

Settings is the self-service area of your account — one page where you manage who you are on the site, how secure your login is, and how much the site contacts you. From it you can edit your public profile, change your password, set up two-factor authentication, choose your notifications, receive stories by e-mail, adjust how the site looks, connect outside accounts like Mastodon and GitHub, invite a new member, and deactivate your account if you decide to leave. It's available only while you're logged in.

---

## Key Capabilities

- Edit your public profile: username, e-mail, an option to show your e-mail, homepage, and an about section
- Change your password — afterwards, every other device where you were logged in is signed out for safety
- Enroll in two-factor authentication by scanning a QR code with an authenticator app (or typing in a revealed secret), and disable it again with your password
- Choose how you hear about comment replies, mentions, and private messages — by e-mail, in your inbox, or as Pushover push alerts
- Turn on mailing-list mode to get all stories and comments, or only stories, delivered to a private personal e-mail address
- Set appearance preferences: color scheme, contrast, story previews, and user avatars
- Connect your Mastodon or GitHub account to your profile, and subscribe to Pushover
- Send an invitation to a new user, and deactivate your account with an option to disown your stories and comments

---

## How It Works

1. **Open Settings while logged in** — everything is on a single page, saved with the **Save Account Settings** button (it appears twice; both save the same form) and confirmed with "Successfully updated settings."
2. **Ordinary changes save directly** — profile fields, notifications, appearance, and mailing-list choices don't ask for your password.
3. **Sensitive changes need your current password** — setting a new password, turning two-factor authentication on or off, and deactivating your account all require it. After a password change your session is renewed, which signs you out everywhere else.
4. **Two-factor enrollment is a short guided flow** — confirm your password, scan the QR code (or reveal the secret and enter it manually), then type the six-digit code from your app and press **Verify and Enable**. You have 15 minutes to finish before the enrollment times out.
5. **Connecting outside services is approve-and-return** — for Mastodon, GitHub, or Pushover you're sent to the other service to approve, then land back on Settings. For Mastodon you first enter your instance in the **Name or URL** box — a hostname like `mastodon.social`, a full URL, or your `@you@instance` handle all work.
6. **Leaving is deliberate** — deactivation asks for your password and an "I am sure" checkbox. Your username stays reserved and your submitted stories are preserved for the community; if you tick the disown option, your stories and comments are relisted under the generic "inactive-user" name. Deactivations (like username renames) are recorded in the public moderation log.

---

## Common Questions

**Q: Why is the site asking for my current password when I only changed a checkbox?**
A: That happens when something — often your browser's autofill — has filled in the New Password field, which switches the save into a password change. Clear both password fields and save again, or enter your current password.

**Q: I changed my password and got signed out on my phone and tablet. Is something wrong?**
A: No — that's intentional. Changing your password (and enabling two-factor authentication) renews your login session, which signs out all other devices. It protects you if someone else had access to your account.

**Q: Can I rename my account?**
A: Yes. Be aware that renames are public: the moderation log records an entry like "changed own username from 'X' to 'Y'".

**Q: What happens if I'm slow setting up two-factor authentication?**
A: The enrollment window is 15 minutes from the moment you confirm your password. If you take longer you'll see "Your enrollment period timed out." — just start again and finish in one sitting.

**Q: I typed the six-digit code and got "Your TOTP code was invalid…"**
A: Codes rotate frequently; re-check the current code in your authenticator app and try again.

**Q: What access does the site get when I connect Mastodon?**
A: Only read access to your account identity (the "read accounts" permission) — enough to confirm who you are. When you disconnect, the site asks your instance to cancel the authorization; if your instance has disappeared, the link is still removed on this side.

**Q: I got "Invalid OAuth state" while connecting Mastodon or GitHub. What now?**
A: The approval came back from a stale tab or an interrupted session. Return to Settings and run the connect flow again from start to finish in one browser session.

**Q: Mastodon connect failed with "isn't resolving to an IP, check for typos?"**
A: The instance name you entered doesn't exist as typed. Re-enter it — a hostname, full URL, or `@you@instance` handle are all accepted. Similar messages ("is X a Mastodon instance?", "isn't a working SSL server") mean the server at that address isn't a working Mastodon instance.

**Q: Can I switch off e-mails about messages from moderators?**
A: No. That notification is always on — the checkbox is shown ticked and locked.

**Q: Is deactivating my account permanent?**
A: Your account stops working immediately, but it can be reactivated through a password reset. Your username stays reserved for you, and your submitted stories remain on the site either under your name or, if you chose to disown them, under "inactive-user".

---

## Tips & Best Practices

- Finish two-factor enrollment within its 15-minute window, in one sitting, with your authenticator app already installed.
- When enrolling, use the "reveal secret" option to store a manual copy of the secret somewhere safe — it's your backup if you lose the device.
- If a save unexpectedly demands your password, check the New Password field for browser autofill before assuming something is broken.
- Avatars come from the Gravatar service for your e-mail address; after changing your picture there, use **Expire cache** in the External Accounts section to refresh it.
- If you use a disposable e-mail address, change it — the form warns you, and such domains don't receive site e-mail.
- Pushover push alerts work once you've subscribed via the Pushover option under External Accounts; subscribe first, then pick which alerts you want.

---

## Limitations & Important Notes

- Two-factor authentication uses authenticator-app codes (TOTP) only.
- Moderator-message e-mail notifications cannot be turned off.
- The Pushover, Mastodon, and GitHub options only appear if this site has those integrations enabled.
- Username renames and account deactivations are recorded in the public moderation log — they are not anonymous.
- When you disconnect GitHub, the site asks GitHub to cancel the authorization; if GitHub's side fails, you'll see a notice asking you to remove it manually in your GitHub application settings.
- Everything on the page saves immediately when you submit — there is no draft state, and both save buttons submit the same form.

---

## Related Features

- **Login & Password Reset** — two-factor codes enrolled here are checked at login; a password reset is also the way to reactivate a deactivated account.
- **Your Profile** — displays the profile fields and the linked Mastodon/GitHub accounts you manage here.
- **Messages, Comments & Inbox** — the activities your notification choices control.
- **Invitations** — the invite form on this page follows your account's invitation privileges; if you can't invite, the reason is shown.
- **Tag Filters** — stories you've filtered by tag are excluded from mailing-list delivery.
- **Moderation Log** — the public record of renames and deactivations.
