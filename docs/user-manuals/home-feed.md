# Home Feed -- User Manual

> Step-by-step instructions for using the different feed views on Lobsters.

---

## Prerequisites

- No account required to browse feeds
- Logging in enables personalized features (hidden stories, saved stories, upvoted stories, tag filters, and the "last read" marker)

---

## Overview

The home feed is where you browse stories on Lobsters. Multiple feed views are available, each presenting stories in a different order: hottest (the default front page), newest, active discussions, recent stories that missed the front page, and top stories by time period. Feeds respect your tag filters.

---

## Task 1: Browse the Front Page (Hottest)

### Steps

1. Navigate to the site home page.
2. Stories are ranked by a hotness algorithm that considers votes, comment activity, and age.
3. Click the story title to read the linked article, or click the **comments** link to see the discussion.
4. Click **Page 2**, **Page 3**, etc. at the bottom to see more stories.

### Expected Result

You see the top-ranked stories. Stories matching your tag filters are excluded.

---

## Task 2: Browse Newest Stories

### Steps

1. Click **Newest** in the site header navigation.
2. Stories appear in reverse chronological order (newest first).

### Expected Result

You see all stories including those not yet popular enough for the front page. A **Last Read** marker shows where you left off on your previous visit.

---

## Task 3: Browse Active Discussions

### Steps

1. Click **Active** in the site header navigation.

### Expected Result

Stories are sorted by the time of their most recent comment. This view highlights ongoing conversations.

---

## Task 4: Browse Recent Stories

### Steps

1. Click **Recent** in the site header navigation.

### Expected Result

You see stories from the last 10 days that have not reached the front page. This is useful for discovering content that may have been overlooked.

---

## Task 5: Browse Top Stories by Time Period

### Steps

1. Click **Top** in the site header navigation.
2. By default, you see the top stories from the past week.
3. Change the time period by modifying the URL:
   - Use **1d** for the past day
   - Use **1w** for the past week (default)
   - Use **1m** for the past month
   - Use **1y** for the past year
   - Use a number prefix for multiples (e.g., **3m** for three months)

### Expected Result

Stories are sorted by score within the specified time period.

---

## Task 6: View Your Saved Stories

### Steps

1. Click **Saved** in the site header navigation.

### Expected Result

You see all stories you have saved, sorted by hotness. This list is private to you.

---

## Task 7: View Your Hidden Stories

### Steps

1. Click **Hidden** in the site header navigation.

### Expected Result

You see all stories you have hidden. Click **unhide** on any story to restore it to your feeds.

---

## Task 8: View Your Upvoted Stories

### Steps

1. Navigate to the upvoted stories page from the header navigation.

### Expected Result

You see all stories you have upvoted (excluding your own stories).

---

## Variations

### Browsing by Domain

Click a domain name that appears next to a story title to see all stories from that domain.

### Browsing by User

Navigate to a user's profile and click their stories link to see all stories submitted by that user.

### RSS Feeds

Most feed views have RSS feeds available. Look for the RSS link in your browser's address bar, or append the RSS format to the URL. If you are logged in, use the RSS URL with your private token (shown on the **Filters** page) to get feeds that respect your tag filters.

---

## Troubleshooting

### A story I submitted does not appear on the front page

**Cause:** Stories need upvotes to rise to the front page. Tags with negative hotness modifiers (such as "meta") push stories lower in the ranking. Your tag filters may also be hiding it.
**Solution:** Check your tag filters. Stories with sufficient upvotes and positive hotness modifiers will appear on the front page over time.

### The "Last Read" marker is missing on the Newest page

**Cause:** The marker only appears if you are logged in and have visited the Newest page before.
**Solution:** Log in and visit the Newest page. The marker will appear on subsequent visits.

### Pages load slowly or show stale content

**Cause:** Feed pages are cached for performance. Anonymous visitors may see content up to 45 seconds old.
**Solution:** Refresh the page. Logging in bypasses the anonymous cache and shows real-time results.
