# Comments — User Manual

> Step-by-step instructions for using Comments.

---

## Prerequisites

- You must be **logged in** to post, reply, vote, or flag (the comment box shows "You must be logged in to leave a comment." otherwise)
- To wear a hat on a comment, a hat must already be granted to your account
- To receive reply/mention emails or push notifications, enable them in your account's notification settings first
- The story must still be accepting comments (older stories close; the box warns when closing is minutes away)

---

## Overview

This guide walks you through posting and replying to comments, editing and deleting your own comments, voting and flagging, following discussions, and the moderator-only actions for removing and restoring comments. It covers the exact time limits the system enforces, so you know what's possible when.

---

## Task 1: Post a comment on a story

### Steps

1. Open the story's page and scroll to the comment box below the story
2. Type your comment (Markdown supported — see the formatting help under the box)
3. (Optional) Click **Preview** to see the rendered comment above the box
4. (Optional) If you have hats, pick one from the **Put on hat:** dropdown
5. Click **Post**

### Expected Result

Your comment appears in the discussion with one point (your own automatic upvote). If the text matched a low-effort pattern (e.g. "+1", "me too", "tl;dr", a bare quote, only emoji), the box shows a rejection message instead — rewrite with substance and post again.

---

## Task 2: Reply to a comment

### Steps

1. Click **reply** in the byline of the comment you're answering
2. Type your reply in the box that opens (the parent comments are shown above it for context)
3. Click **Preview** to check formatting, then click **Post**

### Expected Result

Your reply appears nested under the parent comment. The parent's author gets a notification (and the story's author, if they follow their story). If the thread is 18 levels deep, you'll instead see "Max reply depth reached." — the discussion can't nest further. If the thread has been collecting flags, you may see "Thread speed limit reached, next comment allowed in …" — wait the stated time and post again.

**Note:** you cannot reply to a comment you have flagged, or to a comment that was deleted while you were writing.

---

## Task 3: Edit your comment

### Steps

1. Within **6 hours** of posting (or of your last edit), click **edit** in your comment's byline
2. Change the text; you can also change or remove the hat
3. Click **Preview** to check, then click **Update**

### Expected Result

The comment shows the new text. If you edited more than a minute after posting, the byline now says "edited". After 6 hours the **edit** link disappears and the window cannot be extended.

---

## Task 4: Delete, undelete, or disown your comment

### Steps — Delete (within 14 days)

1. Click **delete** in your comment's byline
2. The comment is replaced by "[Comment removed by author]"

### Steps — Undelete

1. On your deleted comment, click **undelete**
2. The comment is restored with its score

*You cannot undelete a comment a moderator removed.*

### Steps — Disown (after 14 days)

1. On a comment older than 14 days, the **delete** link is replaced by **disown**
2. Click **disown** and confirm

### Expected Result

A disowned comment stays in the thread but is attributed to the site's inactive-user account instead of you. This cannot be undone.

---

## Task 5: Vote and flag

### Steps — Upvote

1. Click the upvote arrow beside the comment (click again to withdraw the vote)

### Steps — Flag

1. Click **flag** in the comment's byline
2. Pick a reason from the dropdown list (a reason is required)

### Expected Result

Flagging records a −1 vote with your reason, visible to moderators. You can only flag comments that are not your own, no older than **7 days**, and not already down at **−10**. After flagging, the comment's score is hidden from you and its **flag** link becomes **unflag**. The comment's author sees how many flags of each type it received — never who flagged.

---

## Task 6: Follow discussions

### Steps

1. Visit the **Newest Comments** page (`/comments`) to see the latest comments site-wide, 20 per page — a **Last Read** line marks where you left off last visit
2. Visit `/comments/upvoted` to review every comment you've upvoted
3. Visit your **Threads** page to re-read the recent discussions you took part in, shown as full threads
4. Subscribe to the RSS feed on these pages; the private feed link (with your personal token) respects your tag filters

### Expected Result

You can monitor discussions without re-opening every story. Comments on stories you've hidden, or tagged with your filtered tags, are excluded from the newest-comments page. Unread replies in threads you follow are marked **(unread)**.

---

## Variations

### Moderators: removing and restoring comments

1. Click **mod delete** in the comment's byline and supply a reason
2. The comment shows "[Comment removed by moderator <your name>: <reason>]", the action is written to the public moderation log, and the author loses karma (2 points per vote the comment had)
3. To restore any removed comment, click **undelete** — restoring someone else's comment is also logged

Moderators can always read removed comment text, always see scores, see flaggers' usernames, and are exempt from the thread speed limit.

### Posting by email

Replies can arrive via the notification email: answer the email and your response is posted to the thread (such comments are marked "e-mailed" in the byline).

---

## Settings & Configuration

Navigate to your account's **Settings** page

| Setting | Description | Default |
|---------|-------------|---------|
| Email me when someone replies | Send reply notifications by email (threaded; reply-able) | off |
| Email me on mentions | Email when someone @mentions you — suppressed if the same comment already emailed you as a reply | off |
| Pushover replies / mentions | Same notifications as phone push | off |
| Tag filters | Filtered tags also drop out of your newest-comments feed | none |
| Hide story | Per-story: stops reply/mention emails and pushes for that story; inbox notifications still accumulate | — |

---

## Troubleshooting

### The **edit** link is missing

**Cause:** More than 6 hours since posting/last edit, the comment was removed, or you're not its author.
**Solution:** None — the window is fixed. For comments older than 14 days, use **disown** if you want to detach your name.

### The **reply** link is missing

**Cause:** You're logged out, the comment was removed, the story stopped accepting comments, or the thread hit the 18-level depth cap.
**Solution:** Log in; for depth or closed stories, consider submitting a new story instead.

### "Thread speed limit reached, next comment allowed in X minutes"

**Cause:** The thread has accumulated flags, so comment pacing is enforced (base 2 minutes, growing with flags; your own flags count double).
**Solution:** Wait the stated time. If the thread is getting heated, step away or flag for moderators.

### "You've flagged that comment for the mods, so you can leave it for the mods."

**Cause:** You're replying to a comment you flagged.
**Solution:** Unflag it if you'd rather engage, or let moderation run its course.

### I didn't receive a reply email

**Cause:** Reply emails are off in Settings, you've hidden the story, or the email failed to send.
**Solution:** Check Settings and your hidden stories. The notification is always in your site inbox regardless.

### A comment shows only "[Comment removed by …]"

**Cause:** The author deleted it, a moderator removed it (name and reason shown), or the author was banned.
**Solution:** Nothing to do — moderators can still see the original if follow-up is needed.

---
