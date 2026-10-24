# Comments — Operations Manual

Operational guide to the commenting system for staff who run the site day to day: what users can and cannot do, the time windows that govern comment actions, the notification pipeline, and the knobs and background tasks that keep it healthy.

## 1. Quick reference: rules and time windows

| Rule | Value | What it governs |
|---|---|---|
| Edit window | 6 hours from last edit | Author may edit their comment; "edited" label appears if edited >1 min after posting |
| Delete window | 14 days from posting | Author may self-delete; afterwards only "disown" is offered |
| Flag window | 7 days from posting | Flagging disabled on older comments |
| Flag floor | score −10 | Comments at/below this can't be flagged further |
| Collapse threshold | score −5 or below | Comment renders collapsed for regular users (moderators see it open) |
| Score hiding | score in −2..4 AND comment <36 h old | Score shows as hidden to non-moderators; also hidden from anyone who flagged it |
| Max reply depth | 18 levels | Reply link disappears; users see the "Max reply depth reached" notice |
| Listing page size | 20 comments | /comments and /comments/upvoted pagination |
| Public RSS cache | 2 minutes | Newest-comments public feed |

## 2. The comment lifecycle from an operations view

1. **Posting.** Only logged-in users can post. The story must still be accepting comments (stories close to new comments after a fixed age; the comment box warns users in the final minutes). The author's own upvote is applied automatically, so every comment starts at score 1.
2. **Automatic content rejection.** The system refuses empty comments, "this"/"me too"/"nice"/"+1", "tl;dr", bumps, quote-only comments, all-caps spaced shouting, and emoji-only comments, each with a tailored error message. These rejections are automatic; no staff action is needed or logged.
3. **Duplicate posts.** If a user resubmits the identical comment (slow connections, double-clicks), the system silently accepts it once — expect no duplicate-comment reports.
4. **Speed limiting in heated threads.** In threads accumulating flags, a user must wait `2 + (flags in the reply chain) + (their own flags, counted again)` minutes between comments in that thread. Moderators are exempt. Users see "Thread speed limit reached, next comment allowed in …", sometimes with "Is this thread getting heated?" appended. This throttle is self-operating; it is a sign a thread may need moderator eyes.
5. **Deep threads.** At depth 18 the system stops accepting replies and quietly files a mod note when users hit the limit — check mod notes if a thread looks like it ended abruptly.

## 3. Removal, restoration, and attribution

- **Author delete (≤14 days):** comment body is replaced by "Comment removed by author" for everyone; moderators can still read the original text in place.
- **Moderator delete:** marks the comment as moderated, writes an entry to the moderation log with the reason you supply, and deducts karma from the author equal to **2 × the number of votes** the comment had. Use the "mod delete" link in the comment byline.
- **Undelete:** moderators can undelete anything; authors can undelete their own deletions but not moderator removals. A moderator undeleting someone else's comment is also logged.
- **Disown (>14 days):** the author transfers the comment to the site's inactive-user account; the content remains but is no longer attributed. This is user-initiated and not a removal.
- **Banned users:** their removed comments render as "Comment from banned user removed".
- Comments cannot be hard-deleted while a moderation record points at them; the moderation log entry is protected.

## 4. Flags and what staff can see

- Flagging requires choosing a reason from the fixed reason list; free-text is not accepted.
- Users cannot flag their own comments, and flagging a comment blocks them from replying to it ("leave it for the mods").
- **Visibility of flag details:** the comment's author sees reason counts only (e.g., "2 troll"); **moderators additionally see the usernames of flaggers**. Treat flagger identities as confidential.
- Flagged-comment scores are hidden from the flagger to discourage retaliatory feuds.

## 5. Notification pipeline

Comment notifications are delivered by a background job after each post; email or push failures are swallowed silently rather than retried, so occasional missing emails are expected behavior, not an incident.

Who gets notified about a new comment:

- The **story's author**, if they follow their story's replies and didn't write the comment themselves.
- The **parent comment's author**, if active and not the commenter.
- Every **@mentioned** active user (also `~username`), except the author and anyone already notified as a reply recipient — reply notifications take precedence over mention notifications to avoid duplicate email.

Each recipient gets an in-app notification unconditionally. **Email and Pushover are additionally gated** by the user's personal settings and are suppressed for users who have hidden the story (the in-app notification still accrues so unhiding reveals it). Reply emails carry proper threading headers, so support questions about "broken email threads" usually trace back to the user's mail client. Users can reply to the notification email to post a comment.

Per-story reply following can be switched off and on per user ("hide replies" / "unhide replies"), which operations can use to explain "why did I stop getting reply emails for this story".

## 6. Read tracking

- The **"Last Read" line** on the newest-comments page is driven by each user's last visit timestamp and carries across pagination.
- Per-story **(unread)** markers come from read ribbons — one per user per story, bumped on each story view.
- **Maintenance:** ribbons untouched for **1 year** are purged by `ReadRibbon.expire_old_ribbons!`. Ensure this runs periodically; unbounded ribbons grow with users × stories.

## 7. Scheduled/background tasks to keep running

| Task | Cadence | Purpose | If it stops |
|---|---|---|---|
| `CommentStat.daily_fill!` | Daily (covers trailing 30 days, so missed runs self-heal) | Stores each day's average comment score for "above average" comment queries | Above-average listings silently fall back to a default average of 3 |
| `ReadRibbon.expire_old_ribbons!` | Periodic (e.g., weekly) | Deletes read ribbons idle >1 year | Table bloat; no user-visible breakage |
| Notification job queue (default queue) | Continuous | Reply/mention delivery | In-app, email, and push notifications stall |

## 8. Feeds and caching

- The public newest-comments RSS is cached for 2 minutes; logged-in users with an RSS token get an uncached, personalized feed (respecting their tag filters). The private feed URL contains the user's token — advise users to keep it secret and regenerate if leaked.
- Page caching may be enabled for the comments index and story threads; after emergency content removal, verify the cached pages no longer show the content.
- Comment permalinks (`/c/<id>`) are resolved through a permanent cache entry mapping the comment to its story anchor. Merged stories are followed automatically.

## 9. Known operational quirks

- The upvoted-comments page does not yet exclude comments on stories the user has hidden.
- Simultaneous votes on the same comment can leave its confidence ranking momentarily slightly off; it self-corrects on the next vote.
- Sibling comments with identical confidence are tie-broken deterministically, so thread order is stable across page loads by design — users reporting "comments jumping around" indicates something genuinely wrong.
- Admins can look up comments by numeric database id directly; regular traffic uses short ids only, which prevents enumeration of the comment table.
