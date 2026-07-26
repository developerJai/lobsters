# Domains & Origins

> A comprehensive guide to browsing stories by source website on Lobsters.

---

## What is Domains & Origins?

Every story submitted to Lobsters that links to an external URL is automatically associated with a domain (like `github.com`) and, when configured, an origin (like `github.com/torvalds`). Domains represent the website a link comes from, while origins provide a finer grouping within that website. You can browse all stories from a specific domain or origin, and moderators can ban problematic sources.

---

## Key Capabilities

- Automatic domain extraction from story URLs when submitted
- Origin grouping that breaks down a domain into more specific sources (e.g., different GitHub users)
- Browse all stories from a specific domain
- Browse all stories from a specific origin within a domain
- View story counts and submitter counts for each domain and origin
- RSS feeds for domain and origin story listings
- Moderators can ban or unban domains and origins to block submissions from problematic sources

---

## How It Works

1. When a story is submitted with a URL, the system automatically extracts the domain name (e.g., `github.com` from `https://github.com/torvalds/linux`).
2. If the domain has origin rules configured (set up by moderators), the system also determines the origin. For example, all links to `github.com/torvalds/*` might be grouped under the origin `github.com/torvalds`.
3. To browse stories from a domain, visit the domain page (you can click on a domain name when it appears on a story, or navigate directly).
4. The domain page shows all stories from that domain, along with the total number of stories and unique submitters.
5. If the domain has origins configured, you can drill down to see stories from a specific origin.
6. Origins can span multiple domains. For example, links to `foo.github.io` and `github.com/foo` can both map to the same origin.
7. Moderators can ban a domain to prevent any future submissions from that website. The ban reason is shown to users who try to submit.
8. Similarly, moderators can ban specific origins without banning the entire domain.

---

## Common Questions

**Q: What is the difference between a domain and an origin?**
A: A domain is the website name (like `github.com`). An origin is a more specific grouping within that domain (like `github.com/torvalds`). Not all domains have origins configured -- it depends on whether moderators have set up grouping rules.

**Q: How do I browse stories from a specific website?**
A: Click on the domain name when it appears next to a story, or navigate directly to the domain page. You will see all stories that link to that website.

**Q: Can I subscribe to stories from a specific domain or origin?**
A: Yes. Domain and origin pages offer RSS feeds that you can subscribe to in your feed reader.

**Q: Why was my story rejected because of a banned domain?**
A: Moderators can ban domains that are known for spam, low-quality content, or other issues. When you try to submit a link to a banned domain, you will see an error message with the ban reason.

**Q: Why was my story rejected as a new user submitting to an unseen domain?**
A: New users (accounts less than 70 days old) cannot submit links to domains that have never appeared on the site before. This is a spam prevention measure. If you believe your link is appropriate, a conversation will be started between you, your inviter, and the moderators so they can review it.

**Q: What does it mean when an origin is banned but the domain is not?**
A: The moderators have blocked submissions from a specific section of a website without blocking the entire site. For example, a specific GitHub user's repositories could be banned while the rest of GitHub remains open.

---

## Tips & Best Practices

- Use domain pages to discover more content from websites you enjoy
- Check the domain page before submitting to see if similar stories from the same source have been posted recently
- If you run a website and notice your domain has been banned, check the moderation log for the reason

---

## Limitations & Important Notes

- Not all domains have origin grouping configured; this is set up manually by moderators
- Banning a domain blocks all future submissions but does not remove existing stories
- New users cannot submit links to domains the site has not seen before
- Domain and origin names are derived automatically from URLs and cannot be manually edited by regular users
- Moderators can configure how URLs are grouped into origins using pattern rules

---

## Related Features

- [Stories](./stories.md) -- Stories are the content that is grouped by domain and origin
- [Home Feed](./home-feed.md) -- Domain and origin pages function as filtered story feeds
- [Search](./search.md) -- Use `domain:` to search for stories from a specific website
- [Moderation](./moderation.md) -- Domain and origin bans are managed by moderators and logged publicly
