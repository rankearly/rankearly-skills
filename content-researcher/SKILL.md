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

# Content Researcher

Research a topic by reading the best-ranking content on the web, distilling it into a structured knowledge base, and surfacing gaps that existing content misses. The output is two files — a knowledge base and a list of under-discussed questions with answers — that together form the foundation for writing superior content.

## Inputs

Provide **one** of the following:

- **Topic** — the subject to research (e.g. "email deliverability", "React performance optimization"). Optionally include **content type** (ultimate guide, how-to, comparison, listicle, tutorial, etc. — defaults to "comprehensive guide").
- **SERP** — a keyword and a list of pages (title + snippet) from a prior SERP analysis. When provided, the source search is skipped entirely.

## Output files

Both files live in the project's current working directory by default. If the user specifies a different location, use that instead.

- `knowledge-base.md` — the knowledge base (~30 entries, each with a depth label)
- `under-discussed.md` — questions not well covered by existing content, with researched answers

## Step 1. Find sources

**If SERP was provided** — use the SERP pages as your source list. Skip to Step 2.

**If topic was provided** — read `./references/search-and-filter.md` for the full search-and-filter process. This produces a list of 5-8 source pages.

## Step 2. Read and extract (subagent per source)

For each selected page, spawn a subagent with the **topic**, a **source ID** (sequential: [1], [2], ...), and the current knowledge base. Read `./references/guide-reader.md` for the subagent prompt. Each subagent reads the page and returns extracted knowledge entries plus discovered questions.

After each page is processed, merge its output into the two shared files.

## Step 3. Answer remaining questions (subagent per question)

Once all sources have been processed, review `under-discussed.md`. For each unanswered question, spawn a subagent. Read `./references/question-researcher.md` for the subagent prompt.
