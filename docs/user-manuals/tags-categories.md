# Tags & Categories -- User Manual

> Step-by-step instructions for filtering stories by tags.

---

## Prerequisites

- No account required to view tags
- Logging in allows your tag filters to persist across browsers and devices
- Anonymous visitors can filter using a browser cookie

---

## Overview

Every story on Lobsters is classified with one or more tags, and each tag belongs to a category (such as "programming", "culture", or "platforms"). You can filter out tags you do not care about so that stories with those tags no longer appear in your feeds.

---

## Task 1: View All Tags

### Steps

1. Click **Tags** in the site header (or navigate to the tags page).
2. Browse the list of all tags, grouped by category.

### Expected Result

You see a table of all active tags with their descriptions, organized under category headings.

---

## Task 2: Browse Stories by a Single Tag

### Steps

1. Click any tag label that appears on a story in any feed.
2. Alternatively, navigate directly by typing the tag name in the URL (e.g., the path for the "security" tag).

### Expected Result

You see a list of stories tagged with that specific tag, sorted by creation date. Related tags are shown at the top of the page.

---

## Task 3: Browse Stories by Multiple Tags

### Steps

1. In the address bar, type a comma-separated list of tag names in the tag URL (e.g., the path for "security,networking").

### Expected Result

You see stories that have any of the specified tags.

---

## Task 4: Filter Out Tags You Do Not Want to See

### Steps

1. Click **Filters** in the site header (or navigate to the filters page).
2. You see a table of all tags grouped by category, with columns for **Hide**, **Tag**, **Description**, **Stories**, and **Filtering**.
3. Check the **Hide** checkbox next to each tag you want to filter out.
4. Scroll to the bottom of the page.
5. Click **Save Filters**.

### Expected Result

A success message confirms "Your filters have been updated." Stories with the filtered tags no longer appear in your feeds. The filter count increases next to each filtered tag.

---

## Task 5: Browse Stories by Category

### Steps

1. Navigate to the category URL directly (categories are groupings of related tags).

### Expected Result

You see all stories that have any tag belonging to that category.

---

## Variations

### Filtering as an Anonymous Visitor

If you are not logged in, your filters are saved in a permanent browser cookie. They work the same way but will not carry over to other browsers or devices. Log in for persistent filters.

### Applying Filters to RSS Feeds

If you are logged in, your tag filters apply to your RSS feeds. Use the RSS URL that includes your private RSS token (visible on the filters page) to get filtered feeds in your reader.

---

## Troubleshooting

### Filtered stories still appear after saving filters

**Cause:** Your browser may be showing a cached version of the page, or you are viewing the site in a different browser where you are not logged in.
**Solution:** Refresh the page. If you are not logged in, make sure you are using the same browser where you set the filters (cookie-based filtering).

### Cannot filter a specific tag

**Cause:** Some tags are marked as "privileged" and can only be filtered by moderators.
**Solution:** This is by design. Privileged tags represent important content categories that cannot be hidden by regular users.

### A tag disappeared from the filter list

**Cause:** The tag may have been deactivated by an administrator.
**Solution:** Inactive tags no longer appear in the filter list and are not applied to new stories. Existing stories keep their tags.
