# Settings

> A comprehensive guide to Settings.

---

## What is Settings?

Settings is your account's home base. It's a single page where you control who you appear to be (username, email, homepage, about text), how secure your account is (password, two-factor authentication), how much the site talks to you (notifications and e-mail delivery), how it looks (light/dark, contrast), which outside services are linked to you (Pushover, Mastodon, GitHub), and — if you ever choose to leave — how your account is closed.

---

## Key Capabilities

- Edit your public profile: username, e-mail, homepage link, and an "about" section
- Change your password (your other logged-in devices are signed out for safety)
- Turn two-factor authentication on or off using any authenticator app
- Pick exactly how you're notified about comment replies, mentions, and private messages — by e-mail, in your inbox, or via Pushover alerts
- Receive newly posted stories (and optionally comments) by e-mail through a private list address
- Choose Light, Dark, or follow-your-System appearance, plus contrast, story previews, and avatars
- Connect or disconnect Mastodon and GitHub accounts shown on your profile
- Invite a new user, and deactivate your account when you want to leave

---

## How It Works

1. **Open Settings** — you must be logged in. Everything lives on one page, organized in sections from profile at the top to account deactivation at the bottom.
2. **Make your changes** — edit fields and tick checkboxes across any sections you like.
3. **Save** — press the save button; a confirmation message tells you the changes took effect. Only one change needs extra proof: setting a *new password* requires your *current* one.
4. **Guided side-trips** — three things step briefly away from the page and bring you back:
   - **Two-factor authentication**: confirm your password, scan a QR code with your authenticator app, type the six-digit code — done. You get 15 minutes to finish.
   - **Connecting services**: for Pushover, Mastodon, or GitHub you approve the connection on the other service's own page and return automatically.
   - **Deactivation**: a separate confirmation form with the consequences spelled out before you commit.

---

## Common Questions

**Q: Why does saving ask for my current password?**
A: Only when you've typed something into the New Password field. Setting a new password always requires the current one; every other setting saves without it. If you didn't mean to change your password, clear those fields and save again.

**Q: I changed my password and got logged out on my other devices. Is that a bug?**
A: No — it's deliberate. Changing your password (or enabling two-factor authentication) signs out every other session, so anyone who had access to your account loses it.

**Q: Can I change my username?**
A: Yes, but renames are recorded in the public moderation log ("changed own username from 'X' to 'Y'"), so the history is visible to everyone.

**Q: What does the 15-minute limit on two-factor setup mean?**
A: After you confirm your password, you have 15 minutes to scan the QR code and enter a valid code. Take longer and you'll see "Your enrollment period timed out" — just start again.

**Q: What does the site get access to when I connect Mastodon?**
A: Read-only access to your account name — enough to confirm who you are and show the link on your profile. The site never posts on your behalf. You can enter your instance as a hostname (`mastodon.social`), a profile URL, or your full `@you@instance` handle.

**Q: Why don't my Pushover checkboxes do anything?**
A: Pushover alerts require an active subscription. Use the Subscribe With Pushover button under External Accounts first; after that the per-event Pushover checkboxes take effect.

**Q: What's the "List Address" shown under Mailing List Settings?**
A: A private, personal e-mail address. When mailing-list mode is on, stories (and optionally comments) are mailed to you "addressed" to it — and anything you e-mail to that address is posted on the site under your name. Treat it like a password.

**Q: Can I turn off e-mails from moderators?**
A: No. E-mail notifications for moderator messages are mandatory; that checkbox is shown ticked and locked.

**Q: Where does my avatar come from?**
A: From the Gravatar linked to your account e-mail. If you change your picture at Gravatar and still see the old one, use the Expire cache link in External Accounts.

**Q: If I deactivate my account, is everything deleted?**
A: Not everything. Your private messages are deleted (recipients keep their copies) and your negatively-scored comments are removed, but your submitted stories remain and your username stays reserved. You can reactivate later by resetting your password. If you'd rather not have content listed under your name, tick "Disown stories/comments" during deactivation and it's relisted under a generic inactive-user name.

---

## Tips & Best Practices

- Finish two-factor setup in one sitting — the QR step expires 15 minutes after your password check.
- Save your authenticator app's secret (the "Reveal Secret" option) somewhere safe when enrolling, so a lost phone doesn't lock you out.
- Keep your mailing-list address private; anyone who has it can post comments as you.
- If your e-mail provider is a disposable-address service, switch it — the site won't deliver mail to blocklisted disposable domains and will warn you on the page.
- Before renaming yourself, remember the rename is publicly logged; pick a name you'll keep.
- Use the System option for color scheme and contrast if you want the site to follow your device's day/night preference automatically.

---

## Limitations & Important Notes

- Two-factor authentication here is app-based (TOTP) only — there's no SMS option.
- Moderator-mail e-mail notifications cannot be disabled.
- Pushover, Mastodon, and GitHub rows appear only if the site has those integrations switched on; if you don't see one, it isn't available on this site.
- Disconnecting Mastodon always works on this site's side, but if your old instance has shut down, its copy of the authorization can't be revoked remotely.
- If GitHub refuses to revoke the connection when you disconnect, you'll be pointed to GitHub's own applications page to remove it manually.
- Deactivation blocks login immediately; reactivation is self-service via password reset, but deleted private messages are not restored.

---

## Related Features

- **Filtered Tags** — stories matching your tag filters are excluded from your mailing-list e-mails.
- **Your Threads** — the "show comments on your submitted stories" setting controls what appears there.
- **Private Messages, Replies & Mentions** — the events your notification checkboxes govern.
- **Invitations** — the invite-a-new-user form lives on the Settings page and follows your account's invitation privileges.
- **Public Profile** — most profile fields and linked accounts you edit here are displayed there.
