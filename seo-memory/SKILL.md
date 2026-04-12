---
name: seo-memory
description: Maintain a project knowledge file for SEO content creation. Use when the user shares critical context about their project — product renames, new/removed features, service changes, subproduct launches, pricing updates, audience shifts, or any factual change that SEO content should reflect. Also triggers on "update seo memory", "remember this for content", or when the user corrects a factual detail about their product/service. Even small updates matter — stale project facts in published content erode trust.
metadata:
  displayName: SEO Memory
  status: live
  phases:
    - name: Load memory
    - name: Determine if update is needed
---

Load project context so content skills have accurate product and audience information.

## 1. Load memory

Read the memory file at `./seo-memory.md`.

- **File exists** — read it and make the context available to downstream skills.
- **File doesn't exist** — ask the user where it is. If they have no preference, create it from the template in `references/template.md` using what they provide. Leave missing sections for later.

## 2. If the user shared business facts, update in a background subagent

Only update for facts that affect what a reader would see — product changes, pricing, positioning, audience. Not implementation details.

(subagent)
Follow `references/update-guide.md` to apply changes to `./seo-memory.md`.
