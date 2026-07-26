# Moderation

> A comprehensive guide to how content and users are moderated on Lobsters.

---

## What is Moderation?

Moderation is how Lobsters maintains the quality of its community. Lobsters prioritizes transparency: every moderation action is recorded in a public log that anyone can view. Moderators have tools to edit or remove content, ban domains and content sources, manage tags, and communicate with users. The system also automatically detects and flags suspicious behavior.

---

## Key Capabilities

- **Public moderation log** visible to all users, showing every moderation action taken
- **Flagged content views** for moderators to review stories and comments that have been flagged by the community
- **Story management** -- moderators can edit, delete, and undelete stories with mandatory reasons
- **Comment deletion** by moderators with reason tracking
- **Domain and source banning** to block submissions from specific websites
- **Tag management** (administrators only) to create and edit tags
- **User management** including banning, unbanning, and invitation privilege control
- **Moderator notes** on users for internal record-keeping
- **Automated detection** of suspicious behavior (banned user login attempts, spam domain submissions, potential brigading)
- **Private notifications** sent automatically to users whose content is moderated, explaining what happened and why

---

## How It Works

1. Community members flag stories and comments they find problematic (off-topic, spam, broken links, unkind, etc.).
2. Moderators review flagged content through the moderator dashboard, which shows flagged stories, flagged comments, and users who receive an unusual number of flags.
3. When a moderator edits or deletes a story, they must provide a reason (unless it is their own story). The action and reason are recorded in the public moderation log.
4. The affected user receives an automated private message explaining what was changed and why.
5. When a moderator deletes a comment, the action is logged and the comment author is notified.
6. Moderators can ban or unban entire website domains or specific content sources. Stories from banned sources are rejected on submission.
7. All moderation actions -- story edits, deletions, tag changes, domain bans, user bans, and more -- appear in the public moderation log, which can be filtered by moderator or action type.
8. The system automatically creates internal notes when suspicious activity is detected, such as when a banned user tries to log in or when a new user tries to submit from a domain that has never been seen before.

---

## Common Questions

**Q: Can I see what moderators have done?**
A: Yes. The moderation log is completely public. Visit the Moderations page to see every action, including who did it and why.

**Q: What happens when my story or comment is moderated?**
A: You receive a private message explaining what was changed (for stories) or that your comment was moderated. The message includes the moderator's reason.

**Q: Why was my story deleted?**
A: Stories can be deleted for being off-topic, duplicate, spam, or for other reasons. Check the private message you received and the public moderation log for details.

**Q: Can moderators edit my story without telling me?**
A: No. Every edit is logged publicly and you receive a notification. The moderation log shows exactly what was changed.

**Q: What are "tag suggestions" vs. moderator edits?**
A: Community members can suggest different tags or titles for stories. If enough users (currently two) suggest the same change, it is applied automatically. These community-driven changes are also logged in the moderation log, noted as coming from "user suggestions" rather than a specific moderator.

**Q: How do domain bans work?**
A: When a moderator bans a domain, any future story submissions linking to that domain are rejected. The ban reason is shown to the user attempting to submit. Existing stories from the banned domain remain visible.

**Q: Can I appeal a moderation decision?**
A: You can reply to the automated notification message to discuss the decision with the moderator. The moderation log is public, so the community can also hold moderators accountable.

---

## Tips & Best Practices

- Check the public moderation log if you are curious about how the site is managed
- If your content is moderated, read the notification carefully to understand why
- Flag content constructively -- your flags help moderators identify real problems
- Remember that community tag and title suggestions are not moderator actions; they come from fellow users

---

## Limitations & Important Notes

- Only moderators can edit or delete other users' stories and comments
- Only administrators can create or edit tags and reparent users in the invitation tree
- The moderation log is never edited or deleted, even if an entry contains an error
- Automated notifications are sent for story and comment moderation, but not for user-level actions like banning
- Banned users receive a ban notification email (not a private message, since they cannot log in to read messages)
- The public IP ban list is separate from the moderation log and shows server-level bans

---

## Related Features

- [Stories](./stories.md) -- Stories can be edited, deleted, and undeleted by moderators
- [Comments](./comments.md) -- Comments can be deleted by moderators
- [Tags & Categories](./tags-categories.md) -- Tags are managed by administrators through the moderation tools
- [Domains & Origins](./domains-origins.md) -- Domains and content sources can be banned by moderators
- [Users](./users.md) -- User banning, unbanning, and invitation management are moderation functions
- [Mod Mail](./mod-mail.md) -- Moderator mail threads appear alongside moderation activity
- [Messages](./messages.md) -- Moderation actions trigger automated messages to affected users
