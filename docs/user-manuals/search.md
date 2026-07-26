# Search -- User Manual

> Step-by-step instructions for finding stories and comments using the search feature on Lobsters.

---

## Prerequisites

- No account required to use search
- Logging in enables additional features such as searching within your filtered tags

---

## Overview

The search feature lets you find stories and comments across the entire site. You can search using plain keywords or use special operators to narrow results by tag, domain, submitter, commenter, title, or user mentions. Results can be sorted by newest, relevance, or score, and you can choose to search stories, comments, or both.

---

## Task 1: Search for Stories by Keyword

### Steps

1. Click **Search** in the site header (or navigate to the search page).
2. Enter your search terms in the search field.
3. Make sure the **Stories** option is selected under the search field.
4. Click **Search**.

### Expected Result

A list of stories matching your keywords is displayed. By default, results are sorted by relevance.

---

## Task 2: Search for Comments by Keyword

### Steps

1. Navigate to the search page.
2. Enter your search terms in the search field.
3. Select the **Comments** option under the search field.
4. Click **Search**.

### Expected Result

A list of comments matching your keywords is displayed, with links to the stories they belong to.

---

## Task 3: Search by Tag

### Steps

1. Navigate to the search page.
2. In the search field, type **tag:** followed by the tag name (e.g., **tag:security**).
3. Click **Search**.

### Expected Result

Results are filtered to only include stories that have the specified tag.

---

## Task 4: Search by Domain

### Steps

1. Navigate to the search page.
2. In the search field, type **domain:** followed by the domain name (e.g., **domain:example.com**).
3. Click **Search**.

### Expected Result

Results are filtered to only include stories linking to the specified domain.

---

## Task 5: Search by Submitter

### Steps

1. Navigate to the search page.
2. In the search field, type **submitter:** followed by a username (e.g., **submitter:alice**).
3. You can combine this with other keywords (e.g., **submitter:alice security**).
4. Click **Search**.

### Expected Result

Results are filtered to stories submitted by the specified user. If you included additional keywords, only matching stories from that user are shown.

---

## Task 6: Search for an Exact Phrase

### Steps

1. Navigate to the search page.
2. In the search field, enclose your phrase in quotation marks (e.g., **"machine learning"**).
3. Click **Search**.

### Expected Result

Results include only stories or comments containing the exact phrase you entered.

---

## Task 7: Change the Sort Order of Results

### Steps

1. Perform a search (see any of the tasks above).
2. Below the search field, select a sort option:
   - **Newest** to see the most recent results first.
   - **Relevance** to see the best matches first (default).
   - **Score** to see the highest-scored results first.
3. Click **Search** again to apply the new sort order.

### Expected Result

The search results are re-ordered according to your selected sort preference.

---

## Task 8: Use Multiple Operators Together

### Steps

1. Navigate to the search page.
2. Combine multiple operators in the search field. For example:
   - **tag:python submitter:bob** to find stories tagged "python" submitted by the user "bob."
   - **domain:github.com security** to find stories from GitHub matching the keyword "security."
   - **title:introduction tag:programming** to find stories with "introduction" in the title that are tagged "programming."
3. Click **Search**.

### Expected Result

Results match all of the specified criteria simultaneously.

---

## Variations

### Searching by Title Only

Use the **title:** operator to restrict your search to story titles. For example, **title:beginner** finds stories with "beginner" in the title.

### Searching by Commenter

Use the **commenter:** operator to find comments by a specific user. For example, **commenter:carol** shows comments posted by the user "carol."

### Searching for User Mentions

Type **@** followed by a username (e.g., **@dave**) to find comments that mention that user.

### Searching by URL

Paste a full URL into the search field to find stories that link to that specific page.

---

## Troubleshooting

### Search returns no results for a term you know exists

**Cause:** Very short words (typically fewer than 3 characters) may be ignored by the search engine. Common words may also be excluded as stop words.
**Solution:** Try using a longer or more specific keyword. Combine it with an operator like **tag:** or **domain:** to narrow the search differently.

### Operators are not filtering results as expected

**Cause:** There may be a typo in the operator name or a space between the operator and its value. Operators must be typed exactly (e.g., **tag:security** with no space after the colon).
**Solution:** Ensure there is no space between the operator, the colon, and the value. Valid operators are **tag:**, **domain:**, **submitter:**, **commenter:**, and **title:**.

### Results seem outdated or incomplete

**Cause:** Newly submitted stories or comments may take a short time to appear in search results as the search index updates.
**Solution:** Wait a few minutes and search again. Recently posted content will appear once the index is updated.
