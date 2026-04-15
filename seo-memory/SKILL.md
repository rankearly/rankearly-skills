---
name: seo-memory
description: Maintain a project knowledge file for SEO content creation. Use when the user shares critical context about their project — product renames, new/removed features, service changes, subproduct launches, pricing updates, audience shifts, or any factual change that SEO content should reflect. Also triggers on "update seo memory", "remember this for content", "initialize seo memory from domain", or when the user corrects a factual detail about their product/service. Even small updates matter — stale project facts in published content erode trust.
metadata:
  displayName: SEO Memory
  status: live
  phases:
    - name: Load memory
    - name: Determine if update is needed
---

Load project context so content skills have accurate product and audience information.

## Route

- **Init from domain** — user wants to scrape a site to build seo-memory. Confirm the domain or sitemap URL, then follow `references/init.md`.
- **Load existing** — read `seo-memory.md` at the project root. If missing, ask the user where it is or create from `references/template.md`.
- **Update** — user shared business facts. (subagent) Follow `references/update-guide.md` to apply changes to `seo-memory.md`.
