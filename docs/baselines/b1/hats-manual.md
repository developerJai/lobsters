# Hats — Operations Manual

This manual is for operations staff (moderators and site operators) administering the hats system: reviewing hat requests, editing hats, and doffing them. Hats are verified affiliation badges users wear on comments and private messages.

## Access levels at a glance

| Task | Who can do it |
|---|---|
| View the public hats list (`/hats`) | Anyone, including logged-out visitors |
| Request a hat | Any logged-in user |
| View the hat request queue | Any logged-in user (be aware the queue is not moderator-only) |
| Approve / reject hat requests | Moderators only |
| Edit a hat (rename, change link) | Moderators only |
| Doff a hat | The hat's owner or any moderator |

## 1. Reviewing the request queue

Open the hat requests page. Each pending request displays:

- **User** — the requester, with how long ago the request was made.
- **Hat** — the requested label. The field is editable: you can fix capitalization or wording before approving.
- **Link** — the verification link (email address or URL). Also editable before approval. If it's a URL it is shown clickable.
- **Comment** — the requester's private justification, rendered from Markdown. Only staff see this.

If there is nothing pending, the page reads "No hat requests."

### Verifying a request

The request form asks users to supply an email address at the organization or a URL proving employment, and encourages them to auth their GitHub account and link to where the organization lists it. Prefer requests you can verify instantly that way; otherwise verify via the provided email/URL. Remember the site policy: hats are for people who will **speak officially** — not for commemorating past contributions — and are usually reserved for notable projects and organizations.

## 2. Approving a request

1. Correct the **Hat** and **Link** fields if needed (your edits are saved as part of approval).
2. Enter a **Reason** (required). This text is sent to the requester.
3. Click **Approve Hat Request**.

What happens automatically:

- A new hat is created on the requester's account, recording you as the granter.
- The grant is written to the public moderation log as `Granted hat "<name>"`, including the link if present.
- The requester receives a private message: *Your hat "<name>" has been approved*, with your reason as the body.
- The request is removed from the queue (requests are deleted on decision; no request archive exists).

You'll see the confirmation "Successfully approved hat request."

## 3. Rejecting a request

1. Enter a **Reason** (required) — the requester will read it verbatim.
2. Click **Reject Hat Request** (shown as a destructive action).

The requester receives a private message *Your request for hat "<name>" has been rejected* containing your reason, and the request is deleted. You'll see "Successfully rejected hat request." Nothing is written to the moderation log for rejections.

## 4. Editing an existing hat

From the public hats table, moderators see an **Edit** link beside each hat. The edit form shows the wearer, plus editable **Hat** and **Link** fields, and two different save buttons:

- **Edit In-Place** — mutates the existing hat. Use for typo-level fixes. Every change is written to the public moderation log (`renamed hat "<old>" to "<new>"`, `changed link from "<old>" to "<new>"`), attributed to you against the hat's owner.
- **Doff & Create** — creates a brand-new hat with the new name (preserving the owner, original granter, link, and modlog flag) and retires the old one with the public reason `To replace with "<new name>"`. Use when the affiliation has genuinely changed, so historical posts keep the label they were made under.

Validation failures (e.g., a name over 255 characters) are flashed back on the edit form.

## 5. Doffing a hat

Doff a hat when the wearer can no longer speak for the organization. Owners can self-doff; moderators can doff anyone's hat.

1. Open the doffing form for the hat. It shows the user and the hat.
2. Enter a **Reason** — a short public explanation, like "Left project". Submitting without a reason fails with "You must give a reason for the doffing."
3. Click **Doff Hat**.

Effects:

- The hat is timestamped as doffed and leaves the public hats table (it remains visible on the user's profile, and old posts keep showing it).
- A public moderation log entry `Doffed hat "<name>"` is written with your reason. If the owner self-doffs, the log entry carries no moderator attribution.
- The hat can never be worn again; a returning user must request a new one.

## Operational notes

- **Requests are destroyed on decision.** The only durable traces of a decision are the moderation log entry (approvals and doffings) and the private message to the user. Copy anything you need before deciding.
- **The approval reason doubles as the notification body** — write it to the user, not as an internal note.
- **Queue visibility:** any logged-in user can open the request queue page, though approve/reject actions remain moderator-gated. Treat request comments as semi-private, not secret.
- **Email links are protected for visitors:** if a hat's link is an email address, logged-out visitors only see the domain.
