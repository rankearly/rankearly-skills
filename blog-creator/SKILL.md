---
name: blog-creator
description: Create or rewrite SEO blog posts — handles research, outlining, and full writing. Use when the user wants to write a blog post from scratch, rewrite a thin draft, or turn an existing outline into a full blog. Triggers on "create a blog", "write a blog post", "rewrite this blog", "this draft is too thin", "help me outline", "write from this outline", or when the user provides a topic idea they want to develop into published content.
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

1. Interpret a keyword that matches user input (subagent) — Ref: `references/keyword.md`. Returns: keyword + SERP analysis (title + snippet, search intent, winnability verdict)
2. Find information gain (subagent) — Run /content-researcher with step 1 output so it skips its own search. Returns: `./blogs/<topic>/knowledge-base.md`, `./blogs/<topic>/under-discussed.md`. **Stop and ask user which under-discussed subject to write about.**
3. Create outline (subagent) — Ref: `references/outline.md`. Returns: `./blogs/<topic>/outline.md`. **Stop. Present outline and wait for feedback.**
4. Write blog (subagent) — Ref: `references/write.md`. Returns: `./blogs/<topic>/blog.md`
5. Create illustration images (subagent) — Ref: `references/image.md`

For steps labelled with `(subagent)`, run them as subagents.

## Router

Interpret the user's intent, flexibly route to different steps. We don't have to write from scratch every time.

- Full write/rewrite for a new subject -> step 0
- Write a blog post from an outline -> step 4
- Polish an existing blog without changing the outline -> step 4
- If the draft is thin and more information should be collected -> step 2

This is not an exhaustive list. Decide which step to go based on the actual intent. 
