# Search

> A comprehensive guide to finding stories and comments on Lobsters.

---

## What is Search?

Search lets you find stories and comments across the entire history of Lobsters. You can search by keyword, or use special operators to narrow results by tag, domain, submitter, commenter, title, or URL. Results can be sorted by newest, relevance, or score.

---

## Key Capabilities

- Full-text search of story titles, descriptions, and bodies
- Full-text search of comment text
- Search operators for targeted searches: `tag:`, `domain:`, `submitter:`, `commenter:`, `title:`, and `@username`
- Quoted phrase matching for exact phrases
- Three sort orders: newest first, most relevant, or highest score
- Paginated results (20 per page)
- URL search for finding previously submitted links (logged-in users only)

---

## How It Works

1. Visit the Search page from the site navigation.
2. Enter your search query in the text field. You can use plain keywords or combine them with operators.
3. Choose whether to search stories or comments using the radio buttons.
4. Choose your preferred sort order: newest, relevance, or score.
5. Click "Search" to see results. Results are paginated at 20 per page.
6. Use operators to refine your search:
   - `tag:security` -- find content tagged with "security"
   - `domain:github.com` -- find stories from a specific website
   - `submitter:username` -- find stories submitted by a specific user
   - `commenter:username` or `@username` -- find comments by a specific user
   - `title:keyword` -- search only in story titles
   - Paste a full URL to find if it has been submitted before (requires login)
   - Use quotes for exact phrases: `"machine learning"`

---

## Common Questions

**Q: Why does my search return no results for short words like "Go" or "AI"?**
A: The search engine ignores terms shorter than three characters. To search for short programming language names, use the tag operator instead: `tag:go` or `tag:ai`.

**Q: Why are some common words ignored in my search?**
A: Common words like "the," "for," "how," and "what" are treated as stopwords and are excluded from search. Try using more specific terms or putting phrases in quotes.

**Q: Can I search by URL to check for duplicates?**
A: Yes, but you must be logged in to search by URL. Paste the full URL (starting with http:// or https://) into the search box.

**Q: Can I combine multiple operators?**
A: Yes. For example, `tag:security domain:github.com` will find security-tagged stories from GitHub. However, you cannot use more than one `domain:` operator or more than one `submitter:` operator in a single search.

**Q: What is the difference between searching stories and comments?**
A: When you search stories, the search looks at story titles, descriptions, and bodies. When you search comments, it looks at comment text. Some operators work slightly differently depending on which you choose.

**Q: Can I search for content that does NOT match a term?**
A: Not yet. Negation (using a minus sign like `-term`) is recognized by the search parser but is not currently implemented. Negated terms are silently ignored.

---

## Tips & Best Practices

- Use the `tag:` operator to find content on specific topics
- Search by URL before submitting a story to check if it has already been posted
- Use quotes around multi-word phrases for more precise results
- If a keyword search returns too many results, add a `domain:` or `submitter:` filter to narrow them down
- Try different sort orders: "newest" shows the most recent results, while "relevance" shows the best matches first

---

## Limitations & Important Notes

- Search terms must be at least three characters long
- Common English stopwords are automatically excluded
- You cannot search by URL unless you are logged in
- Negation (minus sign) is not yet functional
- Results are limited to a maximum of 400 matches (20 pages)
- Searching for a tag that does not exist returns no results without an error message

---

## Related Features

- [Stories](./stories.md) -- Search finds stories by title, description, and body text
- [Comments](./comments.md) -- Search finds comments by their text content
- [Tags & Categories](./tags-categories.md) -- Use `tag:` to filter search results by topic
- [Domains & Origins](./domains-origins.md) -- Use `domain:` to filter search results by source website
