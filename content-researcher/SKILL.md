---
name: content-researcher
description: Use when the user wants to research a topic before writing SEO content — ultimate guides, how-to articles, comparisons, listicles, tutorials, or pillar pages. Triggers on phrases like "research X for me", "what do top articles on X cover", "find content gaps about X", "survey existing content on X", or any request to read and analyze what's already ranking for a topic. Also use when the user wants to build a knowledge base from competing content or find under-discussed angles before writing.
metadata:
  displayName: Content Researcher
  status: live
  phases:
    - name: Expand topic into search queries
    - name: Search and filter sources
    - name: Read and extract knowledge
    - name: Answer under-discussed questions
---

# Content Researcher

Research a topic by reading the best-ranking content on the web, distilling it into a structured knowledge base, and surfacing gaps that existing content misses. The output is two files — a knowledge base and a list of under-discussed questions with answers — that together form the foundation for writing superior content.

## Inputs

- **Topic** — the subject to research (e.g. "email deliverability", "React performance optimization")
- **Content type** (optional) — what the user plans to write: ultimate guide, how-to, comparison, listicle, tutorial, etc. Defaults to "comprehensive guide" if not specified. This shapes the search queries and what counts as a good source.

## Output files

Both files live in the project's current working directory by default. If the user specifies a different location, use that instead.

- `knowledge-base.md` — the knowledge base (~30 entries, each with a depth label)
- `under-discussed.md` — questions not well covered by existing content, with researched answers

## Step 1. Expand the topic into search queries

Take the user's topic and content type, then generate five search queries. Each query targets a different angle or entity related to the topic — this ensures you don't just find the same article five times. Tailor the query suffixes to the content type.

**Example** for topic "technical SEO" (ultimate guide):
- `technical SEO ultimate guide`
- `site architecture SEO complete guide`
- `core web vitals optimization guide`
- `crawl budget management comprehensive guide`
- `structured data markup complete tutorial`

**Example** for topic "React vs Vue" (comparison):
- `React vs Vue 2025 comparison`
- `React vs Vue performance benchmark`
- `React vs Vue developer experience comparison`
- `migrating from Vue to React pros cons`
- `React vs Vue for enterprise applications`

**Example** for topic "setting up ESLint" (how-to):
- `how to set up ESLint from scratch`
- `ESLint configuration best practices`
- `ESLint flat config migration guide`
- `ESLint with TypeScript complete setup`
- `ESLint rules recommended setup tutorial`

## Step 2. Search and filter

Web-search each query. From the combined results, select the top 5-8 pages that are genuinely substantive (structured with headings, covering the topic in depth). Skip thin pages — they won't contribute meaningful knowledge. Match source quality to content type: for comparisons, prioritize hands-on benchmarks and experience reports; for how-tos, prioritize step-by-step tutorials with code/screenshots.

## Step 3. Read and extract (subagent per source)

For each selected source, spawn a subagent. Read `./references/guide-reader.md` for the subagent prompt. Each subagent reads the source and returns extracted knowledge entries plus discovered questions.

After each source is processed, merge its output into the two shared files.

## Step 4. Answer remaining questions (subagent per question)

Once all sources have been processed, review `under-discussed.md`. For each unanswered question, spawn a subagent. Read `./references/question-researcher.md` for the subagent prompt.

Append each answer directly below its question in `under-discussed.md`:

```
## {question}

{answer}

Sources: {urls}
```
