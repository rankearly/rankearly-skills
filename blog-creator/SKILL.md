---
name: blog-creator
description: Umbrella skill for ANY blog-related task — research, outline, write, audit, humanize, illustrate. Use when the user mentions blog posts, outlines, drafts, blog images, or wants to audit/humanize/rewrite blog content.
metadata:
  displayName: Blog Creator
  status: live
  phases:
    - name: Gather requirements
    - name: Find information gain
    - name: Select conversion hooks
    - name: Create outline
    - name: Write blog
---

Create an SEO blog post from a keyword, a topic idea, content requirements, or an existing outline.

## Full write flow

1. Interpret a keyword that matches what users want to write (subagent) — Ref: `references/keyword.md`. Result is saved into `{PROJECT_ROOT}/blogs/<topic>/keyword.md'`. This file is required input for all later steps — do not skip.
2. Find information gain (subagent) — Run /content-researcher with step 1 output so it skips its own search. Result is saved into `{PROJECT_ROOT}/blogs/<topic>/knowledge-base.md`, `{PROJECT_ROOT}/blogs/<topic>/under-discussed.md`.
   - If user clearly states what to write, continue creating the outline.
   - Otherwise, suggest users to find an under-discussed angle from `{PROJECT_ROOT}/blogs/<topic>/under-discussed.md`. Stop here and wait for response.
3. Create outline (subagent) — Pass step 1 output to the subagent. Ref: `references/outline.md`. Result: `{PROJECT_ROOT}/blogs/<topic>/outline.md`. **Stop. Present outline and wait for feedback.**
4. Write blog (subagent) — Ref: `references/write.md`. After writing, run the audit-polish loop from `references/audit-blog.md`. Returns: `{PROJECT_ROOT}/blogs/<topic>/blog.md`
5. Create illustration images (subagent) — Ref: `references/image.md`

For steps labelled with `(subagent)`, run them as subagents.

## Router

Interpret the user's intent, flexibly route to different steps. We don't have to write from scratch every time.

- Full write/rewrite for a new subject -> step 1
- Only need keyword/SERP research for a blog topic -> step 1 only (`references/keyword.md`)
- Collect more information / draft is thin -> step 2
- Create or revise an outline -> step 3 (`references/outline.md`)
- Write a blog post from an outline -> step 4
- Polish an existing blog without changing the outline -> step 4
- Audit an outline for quality/completeness -> `references/audit-outline.md`
- Audit a blog draft for quality/completeness -> `references/audit-blog.md`
- Humanize a blog article (remove AI voice, make it sound natural) -> `references/humanizer.md`
- Generate illustration images for a finished blog -> step 5 (`references/image.md`)
- Add or review conversion hooks -> `references/conversion.md`

This is not an exhaustive list. Decide which step to go based on the actual intent.

## Intermediate research files

`{PROJECT_ROOT}/blogs/<topic>/`
- `keyword.md` — competitive SERP gap analysis
- `knowledge-base.md` — knowledge base
- `under-discussed.md` — questions competitors don't answer well
- `outline.md` — content outline
- `blog.md` — final blog post

Ensure all files exist at the end of research.
