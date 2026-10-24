# Tags & Categories — User Manual

> Step-by-step instructions for using Tags & Categories.

---

## Prerequisites

- Browsing tags and filtering stories requires no special access — anyone can do it, even logged out.
- Creating or editing **categories** requires an **administrator** account.
- Creating or editing **tags** requires access to the moderation area (the links appear on the Tags page when you're signed in as an admin).
- No other setup is needed.

---

## Overview

This guide walks operations staff through maintaining the site's taxonomy — reviewing the tag directory, creating and renaming categories, and managing tags and their availability flags — plus the reader-facing tasks (browsing and filtering) you may need to support. Every taxonomy change you save is recorded in the public moderation log under your name.

---

## Task 1: Review the tag directory

### Steps

1. Navigate to **Tags** (`/tags`).
2. Scan the category headings — categories are listed alphabetically, each heading linking to that category's story feed.
3. Under each heading, review the tags (alphabetical), each showing:
   - the tag link and its description,
   - *inactive* if the tag is retired,
   - **filtered** if your own account filters it (links to your filter settings),
   - **edit** (admins only).
4. As an admin, note the **edit** link beside each category heading, and **Create New Tag** / **Create New Category** at the bottom of the page.

### Expected Result

You have a complete picture of the current taxonomy. The top of the page also reminds readers: "You can filter out stories by tag, even if you don't have an account" and "Inactive tags can no longer be used on new stories."

---

## Task 2: Create a category

### Steps

1. Navigate to **Tags** and click **Create New Category** (admins only).
2. Fill in the required field:
   - **Name** — up to 25 characters; letters, digits, underscores, and hyphens only; must be unique (capitalisation doesn't make it different — `Culture` equals `culture`).
3. Click **Create Category**.

### Expected Result

You're returned to the Tags page with the message "Category *name* has been created", and the new (empty) category is ready to receive tags. The creation is written to the public moderation log. If the name breaks a rule, the save fails with an application error rather than an inline message — double-check the name before submitting.

---

## Task 3: Rename a category

### Steps

1. On the **Tags** page, click **edit** next to the category heading.
2. Change the **Name** field (same rules: ≤25 characters; letters, digits, underscore, hyphen; unique ignoring case).
3. Click **Update Category**.

### Expected Result

You're returned to the Tags page with "Category *name* has been updated". If the new name is invalid, you're sent back to the edit form with the error listed (e.g. "Category not updated: …"). Remember: the category's web address is its name, so renaming changes its link and breaks old bookmarks.

---

## Task 4: Manage a tag

### Steps

1. On the **Tags** page, click **edit** next to the tag (or **Create New Tag** for a new one). This opens the tag screen in the moderation area.
2. Set the fields:
   - **Name** — up to 25 characters; letters, digits, underscore, hyphen, or plus; unique (case matters).
   - **Description** — up to 100 characters; appears next to the tag in the directory.
   - **Category** — the single category the tag belongs to (required).
   - **Active** — untick to retire the tag from new stories.
   - **Privileged** — tick to make the tag moderator-only (applying and filtering).
   - **Permit by new users** — untick to block brand-new accounts from using it.
   - **Is media** — tick for media-type tags (styled differently, excluded from related-tag suggestions).
   - **Hotness mod** — a whole number from −10 to +10 nudging story ranking for this tag.
3. Save.

### Expected Result

The directory reflects your change immediately, and the moderation log records exactly which fields changed from what to what, under your name.

---

## Variations

### Filtering stories by tag (any user, no account needed)

Use this when a reader asks how to hide a topic.

1. Open **Tags** and follow the "filter out stories by tag" link at the top (or the **filtered** marker beside an already-filtered tag).
2. Add or remove tags on the filters page.
3. Stories with filtered tags vanish from the reader's feeds; the Tags page marks those tags **filtered**.

### Reading several tags or categories at once

1. For tags: visit `/t/tag1,tag2` (comma-separated tag names).
2. For categories: visit `/categories/foo,bar`.

### Retiring instead of deleting

There is no delete workflow for tags or categories, and records with history can't be removed. To take a tag out of circulation:

1. Open the tag's **edit** screen.
2. Untick **Active** and save — the tag shows *inactive*, can't be used on new stories, and old stories keep it.

---

## Settings & Configuration

This feature has no settings pages of its own. The relevant per-tag controls live on each tag's edit screen:

| Setting | Description | Default |
|---------|-------------|---------|
| Active | Tag usable on new stories | On |
| Privileged | Moderator-only applying/filtering | Off |
| Permit by new users | Available to brand-new accounts | On |
| Is media | Media-type tag styling/behavior | Off |
| Hotness mod | Ranking adjustment, −10 to +10 | 0 |

---

## Troubleshooting

### The category or tag edit links don't appear

**Cause:** You aren't signed in as an administrator — the links are hidden from ordinary users.
**Solution:** Sign in with an admin account and reload the Tags page.

### Application error when creating a category

**Cause:** The name is too long (over 25 characters), uses invalid characters (spaces or symbols other than `_` and `-`), or duplicates an existing category ignoring case.
**Solution:** Correct the name and submit again.

### "Category not updated: …" after a rename

**Cause:** The new name violates the same naming rules.
**Solution:** Fix the issue named in the message on the edit form and click **Update Category** again.

### A user says they can't apply a tag to their story

**Cause:** The tag is privileged (moderator-only), inactive (retired), or blocked for new accounts.
**Solution:** Apply it on their behalf if appropriate, re-activate the tag, or suggest a current alternative.

### A reader filtered a tag but still sees it in the directory

**Cause:** Filtering hides stories from feeds; the directory always lists all tags, marking filtered ones.
**Solution:** This is expected behavior — point them to the **filtered** marker and the filters page.
