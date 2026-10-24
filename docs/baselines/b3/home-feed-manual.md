# Home Feed — User Manual

> Step-by-step instructions for using the Home Feed.

---

## Prerequisites

- No account is needed to browse feeds or to set tag filters (signed-out filters are saved in a long-lasting browser cookie)
- You must be signed in to use the **Saved**, **Upvoted**, and **Hidden** lists, and to keep your tag filters on your account
- A feed reader (optional) if you want to subscribe to RSS feeds

---

## Overview

This guide walks you through browsing the site's story feeds (front page, Newest, Recent, Active, Top, and tag/category/website views), hiding topics with tag filters, catching up with the Last Read marker, and subscribing to feeds — including private, filtered feeds — from a feed reader.

---

## Task 1: Browse the story feeds

### Steps

1. Open the front page to see the **hottest** stories.
2. Switch views using the site navigation: **Newest** (everything, newest first), **Recent** (newest stories that have not yet reached the front page), **Active** (stories sorted by last comment), or **Top** (best of the past week).
3. On any list, scroll to the bottom and click **Page 2** (and onward) to continue; a **Page 1** style link takes you back.
4. On a story row, click the title to open the link, or the **N comments** link to open its discussion.

### Expected Result

A list of story rows, each showing the score, title, tags, source site, submitter ("via" or "authored by"), age, and comment count.

---

## Task 2: Hide topics with tag filters

### Steps

1. Open the **Filtered Tags** page.
2. Review the table — tags are grouped by category, each with its description, the number of stories carrying it, and how many people filter it.
3. Tick the **Hide** checkbox next to each tag you want to stop seeing. (A tag without a checkbox can't be filtered.)
4. Click **Save Filters**.

### Expected Result

The message "Your filters have been updated." appears and you return to the Filtered Tags page. Stories with those tags no longer appear in any feed you view. If you were signed out, the filters are stored in a long-lasting browser cookie for this browser only.

---

## Task 3: Catch up on Newest with the Last Read marker

### Steps

1. Sign in.
2. Open **Newest**.
3. Read down the list until you reach the **Last Read** divider — stories below it are ones you had already seen on your previous visit.
4. If the divider isn't on the first page, keep clicking the next **Page** link; the marker carries over to later pages.

### Expected Result

A **Last Read** line separates new stories from ones you've seen; your visit updates the marker for next time.

---

## Task 4: View stories for a tag, several tags, or a category

### Steps

1. Click any tag on a story row, or open a tag page directly.
2. Read the header box: the tag's description, any ranking modifier, and special rules (moderator-only tags, tags not permitted for new users), plus "most often also tagged with" suggestions.
3. To combine tags, edit the address and separate tag names with commas; the same works for categories.

### Expected Result

A list of only matching stories. If any name in a comma-separated list doesn't exist, the page returns "not found" — fix the spelling and retry. If you've filtered one of the tags, the page tells you so.

---

## Task 5: Subscribe in a feed reader

### Steps

1. Open the feed you want (front page, **Newest**, **Top**, a tag, a category, or a website page).
2. Use the page's RSS link, or your browser's feed discovery.
3. Signed-in members: for feeds that respect your tag filters, use the token links — the **Filtered Tags** page links to **all stories** and **all comments** private feeds.
4. Paste the URL into your feed reader.

### Expected Result

Your reader shows the feed; private feeds are titled "Private feed for *your-username*", confirming your filters apply. Keep token URLs secret — they identify you.

---

## Variations

### Change the Top page's time period

The Top page defaults to the past week.

1. Open the **Top** page.
2. Edit the address to the period you want — for example `/top/5d` (five days) or `/top/2y` (two years). The page hint lists the units it understands.
3. An unrecognized period redirects you to the one-week default.

### Browse one member's submissions

1. From a member's profile or a story byline, open their newest-stories page.
2. You'll see "Newest stories submitted by *username*" above the list.

### Manage your personal lists (signed in)

- **Save** a story from its row to add it to your **Saved** list (click **unsave** to remove).
- **Hide** a story to remove it from your feeds; visit the **Hidden** list and click **unhide** to restore it.
- Your **Upvoted** list shows everything you've upvoted, most recent votes first.

---

## Settings & Configuration

### Filtered Tags

Navigate to the **Filtered Tags** page.

| Setting | Description | Default |
|---------|-------------|---------|
| Hide (per tag) | Removes stories with this tag from every feed you view | Off |
| Signed-out storage | Filters kept in a long-lasting browser cookie | This browser only |
| Signed-in storage | Filters stored on your account and applied to your private RSS feeds | Across devices |

---

## Troubleshooting

### A story everyone is talking about is missing from my feeds

**Cause:** One of its tags is in your filters, or you hid the story.
**Solution:** Open **Filtered Tags**, untick the tag, click **Save Filters**; or open your **Hidden** list and click **unhide**.

### My filters disappeared

**Cause:** You were signed out and cleared cookies or switched browsers/devices.
**Solution:** Sign in and set your filters again — they'll be stored on your account.

### My feed reader ignores my filters

**Cause:** You subscribed to the public feed URL instead of your private token link.
**Solution:** Re-subscribe using the private links (for example from the Filtered Tags page); the feed title should read "Private feed for *your-username*".

### A multi-tag or category address says "not found"

**Cause:** Every comma-separated name must exist; one typo breaks the whole address.
**Solution:** Check each tag/category name and correct the spelling.

### The front page looks a minute out of date

**Cause:** Signed-out visitors see briefly cached pages (and the front-page feed is cached about two minutes).
**Solution:** Sign in for live, personalized lists, or just wait a moment and refresh.
