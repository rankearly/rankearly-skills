---
name: draft-creator
description: Create SEO content drafts from topic ideas or requirements. Use when the user wants to write a blog post, article, or guide and needs help with research, outlining, and structure. Triggers on "create a draft", "write a blog post", "help me outline", "content brief", or when the user provides a topic idea they want to develop into full content.
metadata:
  displayName: Draft Creator
  status: live
  phases:
    - name: Gather requirements
    - name: Find information gain
    - name: Create outline
---

Create a content draft from a topic idea or content requirements.

## 0. Load Project Context

Look for `./seo-memory.md` (the default seo-memory location).

- **File exists and readable** — load it. Use this context throughout the draft to keep product references, terminology, and positioning accurate.
- **File doesn't exist or inaccessible** — ask the user: "I don't see a project memory file (`seo-memory.md`). Would you like to run `/seo-memory` first to capture your project context? This helps me weave accurate product references into the blog. If not, I'll skip this step."
  - If yes — run the `seo-memory` skill, then continue.
  - If no — proceed without project context.

## 1. Gather Requirements

Ask the user what they want to write about if not provided.

If the input is a vague idea (not full requirements), research reader intent:
1. Try a Google search query likely to find this idea in SERP
2. If SERP is highly related → run `serp-gap-analysis` skill
3. If not related → try another query
4. After 3 failed attempts → stop and report that this may not be a good content idea (no matching searches)

Skip SERP analysis if the input already contains these requirements:
- SERP intent summary
- Word count
- Content format
- Must-have topics
- Competitor gaps

### Required Fields (resolved from input or research)

From SERP analysis:
- SERP intent summary
- Word count
- Content format
- Must-have topics
- Competitor gaps

**Important:** SERP analysis may return multiple options for some fields (e.g., word count ranges like 1. 1500-2500, 2. 2500-3500). Make sure user confirms them before proceeding to the next step.

Propose these based on the above:
- Target reader
- Primary outcome (what the reader can do/understand after reading)

### Setup

Create `./blogs/<topic>/` folder for all writing-related files.

## 2. Find Information Gain (subagent)

Run the `content-researcher` skill. This produces:
- `./blogs/<topic>/knowledge-base.md` — collected knowledge from SERP pages
- `./blogs/<topic>/under-discussed.md` — questions competitors don't answer well

Information gain = what the reader still cannot do, decide, understand, or trust after reading the top results. The under-discussed questions are your information gain.

## 3. Create Outline (subagent)

Use this structure, adapting to content format and word count:

1. **Hook** — grab attention, establish relevance
2. **Problem** — what's at stake, why it matters
3. **Why existing advice is incomplete** — set up your unique angle
4. **Your framework/method** — the core value
5. **Examples/applications** — make it concrete
6. **Mistakes/caveats** — build trust, add depth
7. **Conclusion/next step** — actionable takeaway

### Adapt Based On

- **Word count** — expand or compress sections accordingly
- **Must-have topics** — verify knowledge base has content to cover each
- **Under-discussed questions** — integrate 2-3 as your information gain

### Output Format

```
## {H2 Title}
{1-2 sentence description of what this section covers}
({word count} words)
```

Repeat for each section. Total word counts should match the target.
