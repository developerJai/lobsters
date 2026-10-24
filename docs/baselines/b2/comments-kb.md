# Comments

> **Status**: ✅ Active
> **Generated**: 2026-10-24T00:00:00Z
> **Last Updated**: 2026-10-24T00:00:00Z
---

## Overview

### What It Does
Comments let you join the discussion under any story. You can reply to other people's comments (threads nest up to 18 levels), preview before posting, edit shortly after posting, upvote comments you appreciate, and flag ones that break the rules. When someone replies to you or mentions you, you're notified in your inbox and — if you choose — by email or push notification.

### Why It Exists
The discussions are the heart of the community. Several built-in guardrails (hidden scores on new comments, automatic slow-downs in heated threads, rejection of "me too"-style comments) exist to keep conversations thoughtful.

### Key Capabilities
- Post, preview, and edit comments with Markdown formatting
- Reply in threads; the best-regarded replies rise to the top automatically
- Upvote, un-vote, and flag with a reason
- Delete your comment for 14 days, or disown it afterwards
- Get reply and @mention notifications in your inbox, email, or phone
- Browse the newest comments site-wide, your upvoted comments, and your recent threads

---

## Architecture

### High-Level Design
How a comment travels, in plain terms:

1. You write a comment under a story and press **Post** (or **Preview** first).
2. The site checks it: you must be logged in, the story must still be open for comments, and the comment must pass the quality rules.
3. Your comment appears with one point (your own automatic upvote).
4. In the background, the site notifies the story's author, the person you replied to, and anyone you @mentioned.

### Components
From your point of view the feature has four parts: the **comment box** (with Post, Preview, Cancel, and an optional hat selector), the **comment itself** (byline links for edit, delete, flag, reply), the **listings** (Newest Comments, Upvoted Comments, Your Threads), and **notifications** (inbox, email, Pushover).

### Technology Stack
Not relevant for everyday use — comments work in any browser, and comment emails work with any mail client (replies are threaded properly, and you can answer a notification email to post your reply).

---

## Model Details

### What a comment "knows"
Each comment keeps track of: who wrote it and on which story, which comment it replies to, its text (in Markdown and as displayed), its score and flags, whether it was deleted or removed by a moderator, when it was last edited, and the hat worn with it.

### Rules that apply when you post
- Comments can't be empty, and there's a (very large) length limit.
- Low-effort comments are refused automatically: "this", "me too", "nice", "+1" (just upvote instead), "tl;dr", thread "bumps", comments that only quote someone else, ALL-CAPS-spaced shouting, and emoji-only comments.
- You can't reply to a comment you've flagged, or to a comment that was deleted while you were typing.
- Stories eventually close for comments; the box warns you when closing time is minutes away.
- If a thread is collecting flags, you may have to wait a few minutes between your comments there ("Thread speed limit reached…").

### Key time windows
| Action | Window |
|---|---|
| Edit your comment | 6 hours |
| Delete your comment | 14 days |
| Disown your comment | any time after the 14-day delete window |
| Flag someone's comment | 7 days from when it was posted |

---

## Database Schema
Not applicable for customers — your comments, votes, and notification preferences are stored safely with your account. One detail worth knowing: scores on brand-new comments (less than 36 hours old, score between −2 and +4) are hidden on purpose, to discourage bandwagon voting.

---

## API Endpoints

The pages and actions you'll actually use:

| Where | What you can do |
|---|---|
| Under any story | Write a comment; **Preview** before posting |
| On any comment | **reply**, **upvote**, **flag** (choose a reason), **edit**/**delete** your own |
| `/comments` | Newest comments across the site, 20 per page, with a "Last Read" marker from your previous visit; also an RSS feed (including a private personalized one) |
| `/comments/upvoted` | Every comment you've upvoted |
| Your threads page | The recent discussions you took part in, shown as full threads |
| A comment's timestamp link | Permanent link that always finds the comment, even if stories were merged |

---

## Authorization

What you're allowed to do, in plain language:

- **Anyone logged in** can comment, reply, upvote, and flag (with limits below).
- **Only you** can edit (within 6 hours), delete (within 14 days), or disown your own comments.
- You **cannot flag** your own comments, comments older than 7 days, or comments already voted down to −10.
- If you deleted your own comment, you can undelete it — unless a moderator removed it.
- **Moderators** can remove any comment (shown as "Comment removed by moderator" with a reason), see hidden scores, and see who flagged what.

---

## Configuration

Your personal settings control the notification side:
- **Email me when someone replies** and **email me on mentions** (reply emails take priority — you won't get two emails for one comment)
- **Pushover** push notifications for replies and mentions
- Hiding a story stops emails and pushes about its comments; your inbox notifications quietly accumulate in case you unhide it
- Your tag filters also filter the newest-comments feed

---

## Usage Examples

**Replying with a hat on:** open the reply box, pick your hat from "Put on hat:", write your reply, press **Post**. The hat appears in your comment's byline.

**Fixing a typo:** click **edit** in your comment's byline within 6 hours. Edits made more than a minute after posting are labeled "edited".

**Walking back a bad take:** click **delete** within 14 days — the comment shows as "removed by author". Changed your mind again? **undelete** restores it.

---

## Testing
Not applicable — use **Preview** to test how your Markdown will render before posting.

---

## Known Issues & Caveats

| Caveat | What it means for you |
|---|---|
| Max reply depth is 18 | Very deep threads stop accepting replies; consider writing a post instead |
| Scores hidden on young comments | Not a bug — scores appear after 36 hours or once they leave the −2..+4 range |
| Flagged-by-you comments hide their score from you | Discourages retaliation voting |
| Upvoted-comments page ignores your hidden stories | You may see comments from stories you hid there |
| Heavily downvoted comments appear collapsed | Score −5 and below; click to expand |

---

## Performance
Listings show 20 comments per page; public RSS refreshes about every two minutes. Private token feeds are always fresh.

---

## Troubleshooting

**The edit link disappeared** — more than 6 hours have passed, or the comment was deleted. The window can't be extended.

**"Thread speed limit reached, next comment allowed in …"** — the thread has accumulated flags, so everyone (except moderators) must pace their replies. Wait the stated time.

**I didn't get a reply email** — check your email notification settings, and whether you hid the story. The reply is still in your site inbox.

**My comment was rejected with a strange message** — messages like "Please just upvote the parent post instead." mean the comment matched a low-effort pattern. Add substance and repost.

---

## Related Features

- **Stories** — every comment lives under a story; old stories close to comments
- **Inbox** — where reply and mention notifications arrive
- **Hats** — wear an affiliation badge on a comment
- **Tag filters** — also filter your newest-comments feed

---

**Generated:** 2026-10-24T00:00:00Z
**Last Updated:** 2026-10-24T00:00:00Z
**Status:** ✅ Active
