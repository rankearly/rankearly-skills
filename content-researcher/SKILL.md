---
name: content-researcher
description: Collect what high-ranking content covers about a topic, surface under-discussed subjects, and discover information gains (unique takes). Use when the user wants to research before writing — "research X for me", "find information gains for X", "find content gaps about X", "what are competitors missing about X", or any request to analyze what's already ranking.
metadata:
  displayName: Content Researcher
  status: live
  phases:
    - name: Find sources
    - name: Read and extract knowledge
    - name: Answer under-discussed questions
---

## Inputs

Accept **one** of:
- **Topic** — the subject to research (e.g. "email deliverability"). Optionally include **content type** (ultimate guide, how-to, comparison, listicle, tutorial — defaults to "comprehensive guide").
- **SERP** — a keyword and a list of pages (title + snippet) from a prior SERP analysis.

## Outputs

- `knowledge-base.md` — structured knowledge (~30 entries, each with a depth label)
- `under-discussed.md` — questions not well covered by existing content, with researched answers

Both go in the working directory by default, or wherever the caller specifies.

## Steps

1. **Find sources** (subagent) — If SERP provided, use those pages and go to step 2. Otherwise, follow `references/search-and-filter.md` to get 5-8 source pages.
2. **Read and extract** (subagent per source) — For each page, spawn a subagent with the topic, a source ID ([1], [2], ...), and the current knowledge base. Follow `references/guide-reader.md`. Merge each subagent's output into the two shared files.
3. **Answer remaining questions** (subagent per question) — Review `under-discussed.md` for unanswered questions. For each, spawn a subagent following `references/question-researcher.md`.

For steps labelled with `(subagent)`, run them as subagents.
