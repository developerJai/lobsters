# Hats — User Manual

> Step-by-step instructions for using Hats.

---

## Prerequisites

- You must be signed in for everything except viewing the public hats list
- Requesting a hat requires only a signed-in account
- Approving, rejecting, and editing hats require moderator status
- Doffing a hat requires being the hat's owner or a moderator
- Optional but recommended before requesting: connect your GitHub account under **Settings** (external accounts section)

---

## Overview

This guide walks users through requesting a hat (a verified affiliation badge worn on comments and private messages), and walks moderators through reviewing requests, editing hats, and doffing them. Hats signal that a post speaks officially for a project, organization, or company.

---

## Task 1: Request a Hat

### Steps

1. Navigate to the **Hats** page
2. Click **Request Hat** (shown near the top of the page when you're signed in)
3. Fill in the required fields:
   - **Hat** — the badge text, e.g. "XYZ Project Member"
   - **Link** — public proof of affiliation: "user@project.org, or a URL to an employment page". Shown to users hovering over your hat
   - **Comment** — private justification; "Will only be shown to moderators during approval." Link to discussions where the hat would be useful
4. Click **Request Hat**

### Expected Result

You see the confirmation "Successfully submitted hat request." and are returned to the Hats page. A moderator will review your request; the decision arrives as a private message with the moderator's reason.

---

## Task 2: Review Hat Requests (Moderators)

### Steps

1. Open the **Hat Requests** page. Each pending request shows:
   - **User** — the requester and how long ago they asked
   - **Hat** — the requested label (editable before approval)
   - **Link** — the verification link (editable; clickable when it's a URL)
   - **Comment** — the requester's private justification
2. Verify the affiliation — fastest when the requester has authenticated GitHub and the organization lists that account; otherwise use the email or employment page provided
3. Correct the **Hat** or **Link** fields if needed
4. Enter a **Reason** (required) — this exact text is sent to the requester
5. Click **Approve Hat Request** or **Reject Hat Request**

### Expected Result

- Approve: "Successfully approved hat request." The hat is granted immediately, logged publicly as a grant, and the requester receives the message "Your hat \"…\" has been approved" with your reason.
- Reject: "Successfully rejected hat request." The requester receives "Your request for hat \"…\" has been rejected" with your reason.
- Either way the request leaves the queue permanently. An empty queue shows "No hat requests."

---

## Task 3: Doff (Retire) a Hat

Use when the wearer can no longer speak for the organization. Owners may doff their own hats; moderators may doff anyone's.

### Steps

1. Open the doffing page for the hat (**Doffing a Hat**)
2. Review the displayed **User** and **Hat**
3. Enter a **Reason** — the form hints: Short public explanation, like "Left project"
4. Click **Doff Hat**

### Expected Result

You're taken to the wearer's profile. The hat is retired: it leaves the public hats table, can't be worn again, and the doffing (with your reason) is recorded in the public moderation log. Old posts continue to display the hat.

---

## Task 4: Edit a Hat (Moderators)

### Steps

1. On the **Hats** page, click **Edit** next to the hat (the Edit column appears for moderators only)
2. Update the **Hat** and/or **Link** fields
3. Choose a save mode:
   - Click **Edit In-Place** to change the existing hat — for typo-level fixes
   - Click **Doff & Create** to retire the old hat and grant a fresh one with the new text — for genuine changes of affiliation

### Expected Result

- **Edit In-Place**: you return to the Hats page; the change is publicly logged ("renamed hat … to …" / "changed link from … to …")
- **Doff & Create**: the old hat shows as doffed with the reason "To replace with \"<new name>\"" and the new hat is active, keeping the same owner, original granter, and link

If validation fails (e.g., the name is too long or blank), you're returned to the edit form with the error message.

---

## Variations

### Viewing hats without an account

Anyone can open the **Hats** page. The table lists User, Hat, and Link for every active hat, grouped by hat name. Email-based links appear to signed-out visitors as the domain only; blank links show "None"; doffed hats are omitted (check the user's profile page instead).

### Self-doffing vs. moderator doffing

The steps are identical; the only difference is the public log entry — a self-doff is not attributed to any moderator.

---

## Settings & Configuration

There are no feature-specific settings. One related option:

Navigate to **Settings** (external accounts section)

| Setting | Description | Default |
|---------|-------------|---------|
| GitHub authentication | Linking your GitHub account lets moderators verify your hat request instantly when the organization lists that account | Not connected |

---

## Troubleshooting

### "You must give a reason for the doffing."

**Cause:** The **Reason** field was left blank when doffing.
**Solution:** Enter a short public explanation (e.g., "Left project") and click **Doff Hat** again.

### My hat request form keeps re-rendering

**Cause:** All three fields — **Hat**, **Link**, and **Comment** — are required, and Hat/Link are limited to 255 characters.
**Solution:** Complete every field within the limits and resubmit.

### I can't see an Edit link on the Hats page

**Cause:** The Edit column is only shown to moderators.
**Solution:** Ask a moderator to make the change, or (for your own hat) use the doffing flow.

### A hat still appears on old comments after doffing

**Cause:** By design — history is preserved; doffing only prevents the hat from being worn on new posts.
**Solution:** No action needed.

### Approve/Reject won't submit

**Cause:** The **Reason** field is required for both decisions, and on approval the **Hat** and **Link** fields must be filled.
**Solution:** Complete the required fields and click the decision button again.
