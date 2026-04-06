# Search and Filter Sources (subagent)

Given a topic and content type, find the best-ranking pages to extract knowledge from.

## Step 1. Expand the topic into search queries

Generate five search queries. Each query targets a different angle or entity related to the topic — this ensures you don't just find the same article five times. Tailor the query suffixes to the content type.

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

Web-search each query. From the combined results, select the top 5-8 pages that are **directly about the topic** and genuinely substantive (structured with headings, covering the topic in depth). Skip:
- Thin pages — they won't contribute meaningful knowledge
- Tangentially related pages — even if high-quality, they don't serve the reader's intent
