# Users -- User Manual

> Step-by-step instructions for viewing user profiles and the invitation tree.

---

## Prerequisites

- No account required to view profiles and the invitation tree
- Viewing your own standing page requires logging in

---

## Overview

Every Lobsters user has a public profile page showing their karma, activity stats, hats, and social links. The invitation tree shows how all users are connected through the invitation chain. You can also view your flag standing to understand how your contributions compare to the community.

---

## Task 1: View a User's Profile

### Steps

1. Click any username that appears on the site (next to a story submission, comment, or in any user list).
2. Alternatively, navigate directly to the user's profile URL (e.g., the path with a tilde followed by the username).

### Expected Result

You see the user's profile page displaying:
- **Status** (active user, moderator, administrator, or deactivated/banned)
- **Joined** date and who invited them
- **Karma** score
- **Stories** and **Comments** counts
- **About** bio (if they have written one)
- **Hats** they hold
- Social links (**GitHub**, **Mastodon**, **Homepage**) if configured

---

## Task 2: View the Invitation Tree

### Steps

1. Click **Users** in the site header (or navigate to the users page).
2. The invitation tree shows all users organized by who invited whom.

### Expected Result

You see a hierarchical tree view where each user is listed under the person who invited them. This visualizes the chain of trust in the community.

---

## Task 3: View Users by Karma

### Steps

1. Navigate to the users page.
2. Click the **by karma** link (or add the appropriate parameter to the URL).

### Expected Result

You see a flat list of users sorted by karma score, highest first.

---

## Task 4: View Your Flag Standing

### Steps

1. Log in to your account.
2. Navigate to your own profile page.
3. Click the **standing** link (or navigate to your standing page directly).

### Expected Result

You see a breakdown of your flag statistics compared to the community average, including how often your stories and comments are flagged and how your flagging behavior compares to other users.

---

## Task 5: Send a Message to Another User

### Steps

1. Navigate to the user's profile page.
2. Click **Send a Message** in the sub-navigation area at the top of the page.

### Expected Result

You are taken to the message compose form with the recipient pre-filled.

---

## Variations

### Viewing the Moderators List

Click **Moderators** in the site footer or navigate to the moderators page to see a list of all moderators and administrators.

### Refreshing Your Avatar

Your avatar comes from Gravatar based on your email address. If you change your Gravatar image, go to **Settings** and click **Expire cache** next to the Gravatar section to update your avatar on Lobsters.

---

## Troubleshooting

### "User not found" after someone changed their username

**Cause:** The old username URL no longer works because usernames are looked up by the current name only.
**Solution:** Check the moderation log for username changes. The "not found" page provides a link to search the moderation log for username changes.

### A user's profile shows "User deactivated own account"

**Cause:** The user chose to deactivate their account through the settings page.
**Solution:** No action needed. Their stories and comments remain visible (unless they chose to disown them), but their profile shows limited information.

### Cannot view another user's standing page

**Cause:** The standing page is only visible to the user themselves and moderators.
**Solution:** You can only view your own standing page. Navigate to your own profile and click **standing**.
