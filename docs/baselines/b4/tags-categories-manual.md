# Tags & Categories — User Manual

> Step-by-step instructions for using Tags & Categories.

---

## Prerequisites

- Browsing the tag directory and filtering stories by tag require no special access — you don't even need an account.
- Creating or renaming **categories** requires an **administrator** account.
- Managing **tags** requires access to the moderation area.
- No other setup is needed.

---

## Overview

This guide covers the everyday tasks around the site's topic system: browsing the tag directory, hiding topics you don't want to see, reading several topics at once, and — for operations staff — maintaining the vocabulary of tags and categories. Staff should remember that every change to a tag or category is written to the public moderation log, stating what changed, from what to what, and who did it.

---

## Task 1: Browse the tag directory

### Steps

1. Open the public tag directory page.
2. Scan the category headings — categories are listed alphabetically, each containing its tags.
3. Read the one-line description next to each tag to understand what it's for.
4. Note the status markers:
   - ***inactive*** — the tag is retired and can't be used on new stories (older stories keep it)
   - **filtered** — a tag you currently hide from your own feeds
5. Click any tag or category to open its stories. Tag and category names are also their web addresses.

### Expected Result

You see the full, categorized list of topics with descriptions and status markers, and can jump straight into any topic's stories.

---

## Task 2: Hide a topic from your feeds

### Steps

1. Open the tag directory. The page itself notes: "You can filter out stories by tag, even if you don't have an account."
2. Go to the filters page and pick the tags you want to hide.
3. Return to your feeds.

### Expected Result

Stories carrying the filtered tags stop appearing in your feeds, and the directory marks those tags **filtered** for you — a handy inventory of what you're hiding. No account is required.

---

## Task 3: Read several topics at once

### Steps

1. For multiple tags, visit `/t/tag1,tag2` — list the tag names separated by commas.
2. For whole categories, visit `/categories/foo,bar` — same comma trick with category names.

### Expected Result

A single story list combining all the chosen tags or categories. For discovering what to combine, each tag also offers up to 8 related-tag suggestions — the tags that most often appear on the same stories (the generic catch-all tag and media tags are excluded from suggestions).

---

## Task 4: Create or rename a category (administrators)

### Steps

1. Sign in with an administrator account — category screens are admin-only.
2. Open the category creation or editing screen.
3. Enter the category name following the rules:
   - up to 25 characters;
   - letters, digits, underscore, or hyphen (the plus sign is **not** allowed in category names);
   - must be unique — capitalisation doesn't count, so two names differing only in case are the same category.
4. Save.

### Expected Result

The category appears in the directory and the change is recorded in the public moderation log. **Warning:** an invalid name (too long, bad characters, or a duplicate ignoring case) fails with an application error rather than a friendly message — check the name before saving. Renaming also changes the category's web address, so old links break.

---

## Task 5: Manage a tag (moderation area)

### Steps

1. Open the tag's management screen in the moderation area.
2. Set the tag's name and description:
   - name: up to 25 characters; letters, digits, underscore, hyphen, or plus; case-sensitive;
   - description: up to 100 characters, shown in the directory.
3. Assign the tag to exactly one category.
4. Set the usage rules as needed:
   - **active** — turn off to retire the tag from new stories;
   - **privileged** — moderator-only: only moderators can apply it to stories or filter it;
   - **new-account availability** — some tags can be made unavailable to brand-new accounts;
   - **media** — marks a media-type tag (excluded from related-tag suggestions);
   - **ranking adjustment** — a value from −10 to +10 nudging how stories with this tag rank.
5. Save.

### Expected Result

The directory reflects the change immediately, and the moderation log records exactly what changed and who changed it.

---

## Variations

### Retiring a tag instead of deleting it

Tags and categories are never deleted — retirement is the only removal path.

1. Open the tag in the moderation area.
2. Mark it inactive and save.
3. The tag shows the *inactive* marker, can't be used on new stories, and remains on older stories so history stays readable.

### Submitting a story with restricted tags

Unusable tags are still listed on purpose. If you pick one, you get an explicit error telling you why: the tag is moderator-only, retired, or not yet available to your new account. Choose an alternative tag or ask a moderator to apply a privileged tag.

---

## Settings & Configuration

There is no settings page for readers — your only personal setting is your tag filter list on the filters page.

Per-tag controls (staff, via the moderation area):

| Setting | Description | Default |
|---------|-------------|---------|
| Active | Tag usable on new stories; off = retired | On |
| Privileged | Only moderators can apply or filter the tag | Off |
| New-account availability | Whether brand-new accounts can use the tag | Available |
| Media | Media-type tag; excluded from related suggestions | Off |
| Ranking adjustment | −10 to +10 nudge to story ranking | 0 |

---

## Troubleshooting

### A tag can't be added to a story

**Cause:** The tag is privileged (moderator-only), inactive (retired), or unavailable to brand-new accounts.
**Solution:** Read the error message — it says which rule applied. Pick another tag, or ask a moderator to apply a privileged tag on your behalf.

### Saving a category fails with an application error

**Cause:** The name breaks a rule — over 25 characters, characters other than letters/digits/underscore/hyphen, or it duplicates an existing category ignoring capitalisation.
**Solution:** Correct the name and save again.

### A bookmarked tag or category link stopped working

**Cause:** Names are web addresses; staff renamed the tag or category, which changed its link.
**Solution:** Find the topic again from the directory and update your bookmark.

### A filtered tag still appears in the directory

**Cause:** Filtering hides *stories* from your feeds; the directory always lists every tag and simply marks yours **filtered**.
**Solution:** This is expected. Use the marker to review or change your filter list.

### The category screens won't open

**Cause:** Your account is not an administrator — category management is admin-only.
**Solution:** Sign in with an administrator account.
