# Users

> A comprehensive guide to user profiles, the invitation tree, and account management on Lobsters.

---

## What is Users?

Your user profile is your public identity on Lobsters. It shows your username, karma score, bio, linked social accounts, hats (verified flair), and activity statistics. The invitation tree visualizes the chain of who invited whom, reflecting the trust-based community structure. Moderators and administrators have additional tools for managing user accounts.

---

## Key Capabilities

- Public profile page displaying karma, bio, hats, and social links (GitHub, Mastodon, personal homepage)
- Invitation tree showing the full hierarchy of who invited whom
- User list views sorted by karma or filtered to moderators and administrators
- Standing page showing how your flagging activity compares to the community
- Gravatar-based avatar that updates when you change your email
- Username change with a cooldown period
- Account deletion (soft delete) and content disowning
- JSON profile data available for each user

---

## How It Works

1. Visit any user's profile by navigating to their username link (e.g., clicking on someone's name next to a story or comment).
2. The profile page displays the user's karma, bio, hats, linked social accounts, and submission statistics.
3. To view the full invitation tree, click "Users" in the site navigation. This shows every user and who invited them.
4. You can also view the user list sorted by karma or filter to just moderators and administrators.
5. If you want to check your standing (how your flagging behavior compares to others), visit your own standing page. Moderators can also view any user's standing.
6. Your avatar is pulled from Gravatar based on your email address. If you change your email, you may need to expire your avatar cache in settings for the new image to appear.
7. You can change your username, but only once per year. A username you previously used cannot be claimed by anyone for five years.
8. If you delete your account, your negative-scoring comments are removed, your messages are hidden, and your unused invitations are expired. You can optionally disown all your content, which transfers it to a generic account.

---

## Common Questions

**Q: What information is shown on my public profile?**
A: Your username, karma score, account creation date, bio (if you wrote one), any hats you hold, linked GitHub and Mastodon accounts, your homepage URL, and counts of your stories and comments.

**Q: What is the invitation tree?**
A: The invitation tree is a public visualization showing every user and who invited them. Since Lobsters is invitation-only, every user (except the very first) was invited by someone else, creating a tree of accountability.

**Q: How often can I change my username?**
A: You can change your username once per year. Additionally, any username that was used by anyone in the last five years cannot be claimed, to prevent impersonation.

**Q: What happens when I delete my account?**
A: Your account is soft-deleted: your negative-scoring comments are removed, your sent and received messages are hidden, your unused invitations expire, and your moderation-use hats are retired. You can optionally disown all your content, which transfers authorship to a generic inactive account. You can reactivate your account later through the password reset process.

**Q: What is the "standing" page?**
A: The standing page shows your flagging statistics compared to the rest of the community. It helps you understand whether your comments are being flagged more or less than average. Only you and moderators can see your standing page.

**Q: What does karma represent?**
A: Karma is a score based on how other users vote on your stories and comments. Higher karma unlocks capabilities like suggesting tags and titles (requires 10), flagging comments (requires 50), and viewing invitation requests (requires 50).

---

## Tips & Best Practices

- Fill out your bio and link your social accounts to help the community get to know you
- Check your standing page occasionally to see how your contributions are being received
- If you change your email and your avatar does not update, use the "expire avatar cache" option in your settings
- Think carefully before changing your username, as you can only do it once per year

---

## Limitations & Important Notes

- New users (accounts less than 70 days old) have some restrictions, such as not being able to invite others or use certain tags
- You need at least 10 karma to suggest tag or title changes on stories
- You need at least 50 karma to flag comments
- A karma score below -4 prevents you from submitting stories
- If your account is banned, your inviter may share some responsibility
- Username changes are logged publicly in the moderation log

---

## Related Features

- [Authentication](./authentication.md) -- Login, logout, and password management for your account
- [Signup & Invitations](./signup-invitations.md) -- How new accounts are created through the invitation system
- [Settings](./settings.md) -- Manage your profile, security, and notification preferences
- [Hats](./hats.md) -- Verified flair that appears on your profile and comments
- [Moderation](./moderation.md) -- How moderators manage user accounts and content
