---
name: blog-creator
description: Create SEO blog posts from topic ideas — handles research, outlining, and full writing. Use when the user wants to write a blog post, article, or guide from scratch, or when they have an existing outline and want to turn it into a full blog. Triggers on "create a blog", "write a blog post", "help me outline", "content brief", "write from this outline", or when the user provides a topic idea they want to develop into published content.
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

Create an SEO blog post from a topic idea, content requirements, or an existing outline.

## Intent Routing

Check what the user is asking for:

- **"Write a blog from this outline"** or an outline file is provided → skip to **Step 5**.
- **Everything else** (topic idea, keyword, "write a blog about X") → start from **Step 0**.

## 0. Load Project Context

Run /seo-memory. It handles checking for an existing file, creating one if needed, or skipping.

## 1. Gather Requirements (subagent)

Read `references/requirements-gatherer.md` for the full process.

> **Constraint**: Never use WebSearch in this step. Use /serp-gap-analysis Phase 1 only — it has a specialized SERP API.

**Input**: user's topic idea OR content requirements

**Returns**:
- Keyword
- Search intent (must be related to the topic)
- Winnability (for reference)
- Pages to explore (title + snippet from SERP)

### Setup

Create `./blogs/<topic>/` folder for all writing-related files.

## 2. Find Information Gain (subagent)

Run /content-researcher, passing the SERP from Step 1 (keyword + pages list) so it skips its own search steps and goes straight to reading. This produces:
- `./blogs/<topic>/knowledge-base.md` — collected knowledge from SERP pages
- `./blogs/<topic>/under-discussed.md` — questions competitors don't answer well

Information gain = what the reader still cannot do, decide, understand, or trust after reading the top results. The under-discussed questions are your information gain.

## 3. Select Conversion Hooks (subagent)

If seo-memory was loaded, scan it and pick the pieces that naturally fit this article's topic and reader intent:

- **Offerings** — which capabilities/benefits are directly relevant to the reader's problem?
- **Pricing** — is there a free tier or low-commitment entry point worth mentioning?
- **Audience** — which segment matches the target reader? Use their pain points and goals to frame the narrative.
- **Positioning** — any differentiator that answers a question the reader would naturally ask?

Write a short selection (a few bullet points) into `./blogs/<topic>/conversion-hooks.md` — what you picked and where it fits in the article. These are not ads; they should feel like natural examples, proof points, or recommendations within the content.

If seo-memory was not loaded, skip this step.

## 4. Create Outline (subagent)

Read `references/outline-creator.md` for the full process.

The outline is saved to `./blogs/<topic>/outline.md`.

### User Review

Present the outline to the user and wait for feedback before proceeding. The user may want to:
- Reorder, add, or remove sections
- Adjust the angle or emphasis
- Change the target word count

Apply any requested changes to the outline file, then proceed.

## 5. Write Blog (subagent)

Read `references/blog-writer.md` for the full process.

The blog is saved to `./blogs/<topic>/blog.md`.

## 6. Create Illustration Images (subagent)

Read `references/image-illustrator.md` for the full process.
