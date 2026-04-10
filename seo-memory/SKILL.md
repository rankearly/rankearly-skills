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

Track project knowledge so content skills have accurate product and audience context.

## 1. Locate the memory file

Check for an existing memory file at `./seo-memory.md`.

- **File exists** — read it and proceed to step 2.
- **File doesn't exist / no access** — ask the user where they'd like to store it. If they have no preference, create it at the default path.

For a brand-new file, initialize it with the template in `references/template.md`. Fill sections from what the user provides. If details are missing, leave them for later instead of inventing them.

## 2. Capture the update

Parse what the user shared and place it in the right section.

See the template for section definitions and entry formats. For offerings, connect each capability to a clear customer benefit. Prefer customer-facing language over internal implementation details.

**Deduplication rules:**
- If an existing entry covers the same topic, update it in place — don't create a duplicate.
- We don't track changelog or history of updates. Always maintain the up-to-date information in the file.

## 3. Confirm and summarize

After writing, show a short summary of what changed:

```
Updated seo-memory.md:
- [Offerings > Keyword Explorer] Added benefit: "Find low-competition keywords without manual SERP checking"
- [Pricing] Updated free tier limit from 50 to 100 keywords
```

## Handling bulk context

If the user shares a lot of context at once, break it into the right sections. Keep facts that affect SEO content. Skip internal details that do not matter to readers.
