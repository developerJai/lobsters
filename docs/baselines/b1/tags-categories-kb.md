# Tags & Categories

Everything you need to know about how stories are organized on the site.

## What are tags and categories?

Every story submitted to the site is labelled with one or more **tags** — short keywords like a topic name — so readers can quickly see what a story is about and find more stories on the same subject. Tags are grouped into broader **categories**, so the full list of tags is easy to browse. Each tag belongs to exactly one category.

You can see the complete list at the **Tags** page: tags are shown grouped under their category headings, in alphabetical order, each with a one-line description of what the tag is for.

## What can I do with tags?

- **Browse by tag.** Click any tag to see all stories carrying that tag. You can even combine several tags in one view by visiting `/t/tag1,tag2`.
- **Browse by category.** Click a category heading to see stories across all of that category's tags. Multiple categories can be combined too, with `/categories/foo,bar`.
- **Filter out what you don't want.** If there are topics you'd rather not see, you can filter stories by tag so they no longer appear in your feeds. This works **even if you don't have an account** — the filters page remembers your choices. Tags you currently filter are marked "filtered" on the Tags page, with a shortcut link back to your filter settings.

## How do tags behave?

- **Tag names are short and simple.** A tag is at most 25 characters, using only letters, numbers, underscores, hyphens, or plus signs. Each tag has a short description (up to 100 characters) shown on the Tags page.
- **Some tags are inactive.** Inactive tags can no longer be used on new stories. They remain visible on the Tags page (marked *inactive*) so older stories still make sense.
- **Some tags are reserved.** A few special tags can only be applied by moderators. Everyone can still read stories with those tags.
- **Some tags are restricted for new accounts.** Certain tags can't be used by brand-new users when submitting a story.
- **Tags influence ranking.** Each tag can carry a small boost or penalty that nudges how prominently stories with that tag appear on the front page.
- **Related tags.** The site tracks which tags tend to appear together on the same stories, and can show up to eight tags most related to a given one (the generic catch-all tag and media-type tags are left out of these suggestions).

## Who manages tags and categories?

Creating or renaming tags and categories is an administrator/moderator task. Every change — a new tag, a renamed category, an edited description — is recorded in the public moderation log, so the community can always see what changed, when, and by whom.

Categories are deliberately long-lived: a category that still contains tags cannot be removed, and tags that are no longer wanted are retired (marked inactive) rather than deleted, so old stories keep their labels.

## Frequently asked questions

**Do I need an account to filter tags?**
No. Tag filtering works for logged-out visitors as well.

**Why can't I use a particular tag on my story?**
It may be a privileged tag (moderator-only), an inactive tag (retired from new stories), or a tag not available to brand-new accounts. If you try, you'll get a clear error rather than a silent failure.

**Can a tag belong to two categories?**
No — each tag lives in exactly one category.

**Can tags be deleted?**
Effectively no. Tags are deactivated instead, which keeps the history of older stories intact.

**Is there a machine-readable list of tags?**
Yes — the Tags page is also available as JSON, listing each tag's name, description, category, and status flags.
