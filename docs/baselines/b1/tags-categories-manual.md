# Tags & Categories — Operations Manual

Instructions for operations staff (site administrators and moderators) who maintain the site's tag and category taxonomy.

## Before you start

- **Viewing** the Tags page requires no privileges — it is public.
- **Creating or editing categories** requires an **administrator** account. The category screens reject non-admin users.
- **Creating or editing tags** is done from the moderation area; the Tags page shows the entry links when you are signed in as an admin.
- Be aware that **every** tag or category change you save is written to the public moderation log under your name, including the old and new value of each changed field. There is no silent edit.

## Reviewing the current taxonomy

1. Open the **Tags** page (`/tags`).
2. Tags are listed under their category headings, alphabetically. For each tag you can see:
   - its description,
   - an *inactive* marker if the tag is retired from new stories,
   - a *filtered* marker if your own account filters it,
   - an **edit** link (admins only).
3. Each category heading also carries an **edit** link for admins.
4. At the bottom of the page, admins see **Create New Tag** and **Create New Category** links.

Tip: the page is also available as JSON for audits or scripts; it returns each tag's name, description, category, and flags.

## Creating a category

1. From the Tags page, click **Create New Category** (or go to the new-category screen directly).
2. Enter the **Name**. Rules:
   - maximum 25 characters;
   - letters, digits, underscores, and hyphens only (no spaces, no `+`);
   - must be unique — matching is case-insensitive, so `Culture` and `culture` count as the same name.
3. Click **Create Category**.
4. On success you are returned to the Tags page with the confirmation "Category *name* has been created", and the creation is logged in the moderation log.

Note: if the name violates the rules above, the save fails with an application error rather than a friendly inline message — double-check the name before submitting.

## Renaming a category

1. On the Tags page, click **edit** next to the category heading.
2. Change the **Name** (same rules as above) and click **Update Category**.
3. On success you return to the Tags page with "Category *name* has been updated". If the new name is invalid, you are sent back to the edit form with the error listed.
4. Category URLs use the name itself, so renaming a category changes its address; links to the old name will stop working.

## Managing tags

Tag creation and editing happens in the moderation section (reachable via the **Create New Tag** and per-tag **edit** links on the Tags page). When working with tags, keep these operational rules in mind:

- **Name rules:** max 25 characters; letters, digits, underscore, hyphen, and `+` allowed; uniqueness is case-sensitive.
- **Description:** max 100 characters; shown on the Tags page — keep it a one-line explanation of when to use the tag.
- **Category:** every tag must be assigned to exactly one existing category.
- **Flags you control:**
  - *active* — turn off to retire a tag; inactive tags can no longer be used on new stories but remain visible for old ones;
  - *privileged* — only moderators can apply or filter the tag;
  - *permit by new users* — turn off to stop brand-new accounts using the tag;
  - *is media* — marks a media-type tag (styled differently; excluded from related-tag suggestions);
  - *hotness mod* — ranking adjustment, any whole number from −10 to +10.

## Retiring vs. deleting

Do **not** plan on deleting tags or categories:

- A category that still contains tags cannot be removed.
- A tag that users filter, that has moderation history, or that has suggested taggings cannot be deleted either.
- The supported workflow is to mark the tag **inactive**, which preserves all story history.

## Troubleshooting

| Symptom | Likely cause | What to do |
|---|---|---|
| You can't open the category screens | You are not signed in as an administrator | Sign in with an admin account |
| "New category not created" / application error on create | Name too long, contains invalid characters, or duplicates an existing name (case-insensitive) | Fix the name and retry |
| "Category not updated: …" after editing | Same validation rules as creation | Correct the listed problem; you remain on the edit form |
| A tag shows as *inactive* and users complain they can't use it | The tag was retired | Either re-activate the tag or point users to a current alternative |
| A user reports they cannot apply a tag | Tag is privileged (moderator-only) or restricted for new users | Apply it on their behalf, or explain the restriction |
| A change you made isn't reflected in the moderation log entry's author | The edit was made through a path that didn't record the acting user | Verify you edited via the admin/mod screens, which record your user id |
