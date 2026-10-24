# Home Feed — User Manual

> Step-by-step instructions for using the Home Feed.

---

## Prerequisites

- No account is needed to browse story lists or to set tag filters (signed-out filters are stored in a long-lasting browser cookie, for that browser only)
- You must be signed in to use the **Saved**, **Upvoted**, and **Hidden** lists and to keep your filters on your account
- A feed reader (optional) if you want to subscribe to RSS feeds

---

## Overview

This guide shows you how to browse the site's story lists (front page, Newest, Recent, Active, Top, and views narrowed by tag, category, website, source, or member), how to hide topics with tag filters, how to catch up using the "Last Read" marker, and how to follow lists — including your private filtered feeds — from a feed reader.

---

## Task 1: Browse the story lists

### Steps

1. Open the front page to see the **hottest** stories.
2. Switch to another view: **Newest** (every story in submission order), **Recent** (new stories that haven't reached the front page yet), **Active** (sorted by the latest comment), or **Top** (best of a time period).
3. Scan each row: it shows the story's score, title, tags, source site, submitter, age, and comment count.
4. Use the page links at the bottom of the list to move to the next or previous page.

### Expected Result

A list of stories in your chosen order. Signed-in members also see quick actions on each row — hide, save, flag, or suggest changes.

---

## Task 2: Hide topics with tag filters

### Steps

1. Open the **Filtered Tags** page. Each tag row shows the tag's description, how many stories carry it, and how many people filter it.
2. Tick the **Hide** checkbox next to each topic you want to stop seeing. (A tag without a Hide checkbox can't be filtered.)
3. Save your filters.

### Expected Result

Stories with those tags are removed from every list you view, automatically and site-wide. If you're signed out, the filters are stored in a long-lasting cookie in this browser only; sign in to keep them on your account across devices.

---

## Task 3: Catch up on Newest with the "Last Read" marker

### Steps

1. Sign in.
2. Open **Newest**.
3. Read down the list until you reach the **Last Read** line — it marks the first story you had already seen on your previous visit, so everything above it is new to you.
4. If the line isn't on the first page, continue with the page links; the marker carries over to later pages.

### Expected Result

A clear divider between new stories and ones you've already seen, updated on each visit.

---

## Task 4: View stories for a tag, category, website, or member

### Steps

1. Click a tag on any story row (or open a tag page directly).
2. Read the header: the tag's description, whether it raises or lowers story ranking, any special rules (moderator-only tags, tags not allowed for brand-new members), and suggested related tags.
3. To combine topics, edit the address and separate several tag names — or several category names — with commas.
4. For a particular website or source, open its page to see everything submitted from it, with story and submitter counts and any ban status.
5. For one member, open their newest-submissions page.

### Expected Result

A list containing only matching stories. If any name in a comma-separated list doesn't exist, the page returns "not found" — fix the spelling and retry.

---

## Task 5: Subscribe in a feed reader

### Steps

1. Open the list you want to follow.
2. Copy its RSS link into your feed reader.
3. For a feed that applies your tag filters, use your private token link instead (available for the front page, Newest, Saved, and Upvoted feeds).

### Expected Result

Your reader shows the feed. A private feed is titled "Private feed for *your-username*", confirming your filters are applied. Treat the token link like a password.

---

## Variations

### Change the Top page's time period

The Top page defaults to the best stories of the past week.

1. Open **Top**.
2. Edit the period in the address — for example `/top/5d` for five days or `/top/2y` for two years.
3. An unrecognized period simply redirects you to the one-week view.

### Manage your personal lists (signed in)

- **Save** a story from its row to add it to your **Saved** list — a handy reading queue with its own private feed.
- **Hide** a story to remove it from your lists; open your **Hidden** list to restore it.
- Your **Upvoted** list collects everything you've upvoted.

---

## Settings & Configuration

### Tag filters

Navigate to the **Filtered Tags** page.

| Setting | Description | Default |
|---------|-------------|---------|
| **Hide** (per tag) | Removes stories with this tag from every list you view | Off |
| Signed-out storage | Filters kept in a long-lasting browser cookie | This browser only |
| Signed-in storage | Filters kept on your account and applied to your private feeds | Across devices |

---

## Troubleshooting

### A story everyone can see is missing for me

**Cause:** One of its tags is in your filters, or you hid the story.
**Solution:** Open **Filtered Tags**, untick the tag, and save; or open your **Hidden** list and restore the story.

### My filters disappeared

**Cause:** You were signed out and cleared cookies or switched browsers or devices.
**Solution:** Sign in and set your filters again — they'll be kept on your account.

### My feed reader ignores my filters

**Cause:** You subscribed with the public feed link instead of your private token link.
**Solution:** Re-subscribe using the private link; the feed title should read "Private feed for *your-username*".

### A multi-tag or category address says "not found"

**Cause:** Every comma-separated name must exist; one typo fails the whole page.
**Solution:** Check and correct each name.

### Pages look slightly out of date while signed out

**Cause:** Signed-out visitors see briefly cached pages — lists up to about 45 seconds old and the front-page feed up to about 2 minutes.
**Solution:** This is normal; sign in for always-live lists.

### The Hide checkbox is missing on a tag

**Cause:** That tag can't be filtered; choices for it are ignored even if submitted.
**Solution:** None — this is by design.
