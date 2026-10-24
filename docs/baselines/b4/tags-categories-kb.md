# Tags & Categories

> A comprehensive guide to Tags & Categories.

---

## What is Tags & Categories?

Tags are short labels attached to stories so readers can find content by topic, and categories are the groups those tags are organized into — every tag belongs to exactly one category. A public directory page lists all of them, and you can use it to browse topics, discover related tags, and hide topics you don't want to see.

---

## Key Capabilities

- Browse the public tag directory, grouped by category, with a short description for each tag
- See status markers at a glance: *inactive* for retired tags and "filtered" for tags you currently hide
- Filter stories by tag so they stop appearing in your feeds — this works even without an account
- Read stories across several tags at once (`/t/tag1,tag2`) or several categories at once (`/categories/foo,bar`)
- Get related-tag suggestions: up to 8 tags that most often appear on the same stories
- Staff can create and rename categories and manage tags, with every change publicly audited

---

## How It Works

1. **Staff curate the vocabulary** — administrators create categories and manage tags (tag editing happens in the moderation area). Each tag gets a name, a one-line description, and a home in exactly one category.
2. **Tags carry usage rules** — a tag can be active or retired, moderator-only ("privileged"), unavailable to brand-new accounts, marked as a media tag, and can carry a small ranking adjustment that nudges how stories with that tag rank (anywhere from −10 to +10).
3. **Readers browse the directory** — categories are listed alphabetically, each with its tags and descriptions. Tag and category names are also their web addresses.
4. **Readers tune their feeds** — from the filters page you pick tags to hide; stories carrying them disappear from your feeds, and the directory marks those tags "filtered" for you. The directory itself says it plainly: "You can filter out stories by tag, even if you don't have an account."
5. **Tags retire, never vanish** — a retired tag is marked *inactive*: it can no longer be used on new stories, but it stays on older ones so history remains readable. Neither tags nor categories are ever deleted.
6. **Everything is on the record** — every creation or edit of a tag or category writes an entry to the public moderation log stating what changed, from what to what, and who did it.

---

## Common Questions

**Q: Do I need an account to filter out tags?**
A: No. Filtering stories by tag works even when you're not logged in — the directory page says so at the top.

**Q: Can a tag belong to more than one category?**
A: No. Every tag lives in exactly one category.

**Q: Why can't I add a certain tag to my story?**
A: The tag may be privileged (only moderators can apply it), inactive (retired from new stories), or unavailable to brand-new accounts. Unusable tags are still listed on purpose, so if you try one you get an explicit error rather than a silent failure.

**Q: What does the *inactive* marker mean?**
A: The tag has been retired. It can't be used on new stories any more, but older stories keep it.

**Q: Can I read more than one topic in a single list?**
A: Yes. Visit `/t/tag1,tag2` for several tags at once, or `/categories/foo,bar` for whole categories.

**Q: Do tags affect story ranking?**
A: Slightly. Each tag can carry a ranking adjustment between −10 and +10, so stories with certain tags rank a little higher or lower.

**Q: How do I find topics similar to one I like?**
A: The site suggests up to 8 related tags — the ones that most often appear on the same stories as the tag you're looking at (the generic catch-all tag and media tags are excluded from suggestions).

**Q: Who creates tags and categories, and can I see what they change?**
A: Site staff manage the vocabulary: category screens are admin-only, and tag editing happens in the moderation area. Every change is recorded in the public moderation log.

**Q: What are the rules for names?**
A: Tag names are up to 25 characters using letters, digits, underscore, hyphen, or plus, and are case-sensitive. Category names are also up to 25 characters but don't allow the plus sign, and two names differing only in capitalisation count as the same category. Descriptions are up to 100 characters.

---

## Tips & Best Practices

- Start from the directory when exploring — each tag's one-line description tells you what it's for before you open its stories.
- Build an ad-hoc feed with the comma trick (`/t/tag1,tag2`) instead of fiddling with settings.
- Filter early and freely: no account is needed, and the "filtered" markers on the directory double as an inventory of what you're hiding.
- When a tag is rejected on submission, read the error — it tells you whether the tag is moderator-only, retired, or not yet available to your new account.
- Don't bookmark by tag or category name if staff are reorganizing: names are the web addresses, so a rename changes the link.

---

## Limitations & Important Notes

- Readers can't create or rename tags or categories — that's staff-only, and category management specifically requires an administrator.
- Tags and categories are never deleted; retirement (marking *inactive*) is the only removal path, so expect retired entries in the directory.
- Privileged tags can only be applied — and only be filtered — by moderators.
- Some tags are off-limits to brand-new accounts when submitting stories.
- Renaming a tag or category changes its web address; old links and bookmarks break.
- If an administrator enters an invalid category name (too long, bad characters, or a duplicate ignoring case), the save fails with an application error rather than a friendly message.

---

## Related Features

- **Stories** — tags are applied to stories when they're submitted.
- **Home feeds** — tag feeds, category feeds, and your filter list together shape what the front pages show you.
- **Moderation** — tag editing screens live there, and the public moderation log records every taxonomy change.
