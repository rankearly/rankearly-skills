# SEO Memory Init from Sitemap

Build `seo-memory.md` by scraping the project's public pages.

## 1. Fetch and parse sitemap

Fetch `{domain}/sitemap.xml`. Parse it into a flat list of URLs.

Save the list to `${project-root}/sitemap.md`, one URL per line, formatted as todo items:

```
- [ ] https://example.com/
- [ ] https://example.com/features
- [ ] https://example.com/pricing
```

## 2. Filter URLs

Remove non-content pages: login, signup, auth callbacks, privacy policy, terms of service, cookie policy, legal pages, and similar.

From the remaining URLs, keep at most **30**. Prioritize:

1. Documentation pages (docs, guides, how-it-works)
2. Feature and product pages
3. Pricing pages
4. Landing pages and homepage
5. Blog posts (lowest priority — only include if slots remain)

Only keep URLs that are likely to contain extractable business offerings, audience context, or positioning. Drop generic or utility pages.

## 3. Extract and build seo-memory.md

Follow `update-guide.md` for writing style (benefits, not descriptions). Use `template.md` for structure.

**Main agent**: Fetch and read the root URL (`{domain}/`). Initialize `seo-memory.md` at the project root with the Business section, initial Offerings, and any Audience or Positioning signals visible on the homepage.

**Subagents (parallel)**: Dispatch subagents to read the remaining filtered URLs. Each subagent extracts benefit-driven offerings, audience details, or positioning facts and appends them to `seo-memory.md`. Follow `update-guide.md` — update in place if an entry already covers the same topic.

## 4. Mark progress

As each URL is processed, check it off in `sitemap.md`:

```
- [x] https://example.com/features
- [ ] https://example.com/pricing
```
