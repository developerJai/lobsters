# Home Feed — Knowledge Base Article

This article explains the story feeds you see on the site: what each one shows, how to tailor them with tag filters, and how to follow them from a feed reader.

## What is the home feed?

The home page shows the community's "hottest" stories — a ranked mix of recent submissions and active discussion. Beyond the front page, the same story list comes in several flavors so you can browse the way you prefer: by recency, by activity, by popularity over a time period, or narrowed to a single tag, group of tags, category, or source website.

## The feeds at a glance

| Feed | What it shows |
|---|---|
| Front page | The hottest stories right now |
| Newest | Every story in submission order |
| Recent | The newest stories that have not yet reached the front page |
| Active | Stories sorted by their last comment, to foster active discussions |
| Top | The highest-scoring stories of a time period (past week by default) |
| Tag pages | Stories carrying one tag, or several tags at once |
| Category pages | Stories whose tags belong to one or more categories |
| Domain / source pages | Stories submitted from a particular website or source |
| Newest by user | The latest submissions from one member |
| Saved / Upvoted / Hidden | Your personal lists (sign-in required) |

## Reading the story list

Every feed uses the same list layout. Each story row shows its score and upvote arrow, title, tags, the site it links to, who submitted it ("via" someone, or "authored by" when the submitter wrote it), how long ago, and a link to its comments. Signed-in members also get quick actions on each row: hide, save, flag, suggest changes, and — for stories you submitted — edit. External links include handy cached copies (Archive.org and Ghostarchive).

Lists are paginated: use the "Page N" links at the bottom to move forward and back.

### The "Last Read" marker on Newest

When you're signed in, the Newest feed remembers your last visit and draws a **Last Read** line above the first story you've already seen, so you can catch up quickly. The marker follows you onto later pages if it isn't on the first one.

## Top stories and time periods

The Top page defaults to the past week. You can change the period by editing the address — for example `/top/5d` for five days or `/top/2y` for two years — using day, week, month, and year style units shown in the page's hint.

## Tag, category, and source pages

- A single tag page describes the tag, notes any special rules (some tags are moderator-only; some can't be used by brand-new members), tells you if a tag raises or lowers story ranking, and suggests related tags people often combine with it.
- You can view several tags or several categories at once by listing them separated by commas in the address. If any name in the list doesn't exist, the page returns "not found".
- Domain and source pages show how many stories and submitters a site has, and whether the site has been banned from submissions (with the reason).

## Filtering out tags you don't want

Open the **Filtered Tags** page to hide whole topics from the site:

1. The page lists every active tag, grouped by category, with its description, how many stories carry it, and how many people filter it.
2. Tick **Hide** next to the tags you want to avoid.
3. Click **Save Filters**. You'll see "Your filters have been updated."

Stories carrying a filtered tag disappear from your feeds everywhere on the site. A few special tags can't be filtered.

**Signed out?** Your filters still work — they're kept in a long-lasting browser cookie. They won't follow you to another browser or device, though; sign in to store them permanently on your account.

## Following feeds in a feed reader (RSS)

Almost every feed has an RSS version — the front page, Newest, tag pages, category pages, domain pages, Top, and more. Feed links appear on each page (and in your browser via the page's built-in feed discovery).

If you're signed in, you can get **private feeds** that respect your tag filters: use the RSS links that include your personal token (the Filtered Tags page links to "all stories" and "all comments" versions). The feed title will say "Private feed for *your-username*" so you know your filters are applied. Keep that URL to yourself — it identifies you.

Two quirks worth knowing:

- The Recent page's feed link actually points at the Newest feed, because Recent constantly changes as stories get upvoted onto the front page.
- The public front-page feed is cached for a couple of minutes, so brand-new stories can take a moment to appear in readers.

## Your personal lists

- **Saved** — stories you saved for later. Has its own private RSS feed.
- **Upvoted** — everything you've upvoted, newest votes first. Also available as a private feed.
- **Hidden** — stories you've hidden; visit this list to unhide them.

All three require you to be signed in.

## Common questions

**Why don't I see a story my friend sees?** You may have one of its tags filtered, or you hid the story. Check Filtered Tags and your Hidden list.

**Why does a story show `~` instead of a score?** Scores are hidden on some stories (for example very new or heavily flagged ones) to reduce bandwagon voting.

**Why did the front page not change after I refreshed?** For signed-out visitors, listings are briefly cached (under a minute for pages, about two minutes for the front-page RSS). Sign in to always see live data.

**Can I combine tags?** Yes — separate tag names with commas in the address to see stories matching those tags, and the same works for categories.
