---
name: seo-memory
description: Maintain a project knowledge file for SEO content creation. Use when the user shares critical context about their project — product renames, new/removed features, service changes, subproduct launches, pricing updates, audience shifts, or any factual change that SEO content should reflect. Also triggers on "update seo memory", "remember this for content", or when the user corrects a factual detail about their product/service. Even small updates matter — stale project facts in published content erode trust.
metadata:
  displayName: SEO Memory
  status: live
  phases:
    - name: Locate memory file
    - name: Capture the update
    - name: Confirm and summarize
---

Track project knowledge so every content skill has accurate, up-to-date context about the user's product, service, or business.

## 1. Locate the memory file

Check for an existing memory file at the default path: `./seo-memory.md` (relative to the project root or current working directory).

- **File exists** — read it and proceed to step 2.
- **File doesn't exist / no access** — ask the user where they'd like to store it. If they have no preference, create it at the default path.

For a brand-new file, initialize it with the template in `references/template.md`. Walk the user through each section — ask questions to fill it in rather than leaving empty sections. You don't need to complete every section in one sitting; capture what the user provides and leave the rest for later.

## 2. Capture the update

Parse what the user shared and determine which section it belongs to.

See the template for section definitions and entry formats. The key principle: every offering entry must connect features to **customer benefits**. SEO content is written around what the customer gains, not what the product does internally. When the user describes a feature, always ask or infer: "What does this let the customer do or avoid?"

**Deduplication rules:**
- If an existing entry covers the same topic, update it in place — don't create a duplicate.
- We don't track changelog or history of updates. Always maintain the up-to-date information in the file.

## 3. Confirm and summarize

After writing, show the user a short summary of what was added or changed:

```
Updated seo-memory.md:
- [Offerings > Keyword Explorer] Added benefit: "Find low-competition keywords without manual SERP checking"
- [Pricing] Updated free tier limit from 50 to 100 keywords
```

## Handling bulk context

If the user dumps a large amount of context at once (e.g., "here's our whole product"), break it into entries across the appropriate sections. Prioritize facts that would actually appear in or influence blog content — skip internal implementation details that readers wouldn't care about.
