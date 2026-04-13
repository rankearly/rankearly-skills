# Requirements Gatherer (Subagent)

Validate topic viability via quick SERP analysis and collect the SERP pages for later content research.

## What You Return

- **Keyword** — the search query used
- **Search intent** — the intent from the SERP analysis
- **Winnability** — the verdict from the SERP analysis
- **Pages** — a list of SERP pages from the analysis

If everything that should be returned is already provided in the context, skip the entire process.

## Process

> **NEVER use WebSearch tool.** Use /serp-gap-analysis — it has a specialized SERP API.

1. Determine the keyword to analyze:
   - **Has keyword** — the user explicitly provides a keyword to target. Use it as-is.
     - `create a blog for the keyword "email deliverability"` → keyword: `email deliverability`
   - **No keyword** — the user gives a topic idea without specifying a keyword. Form the most likely Google search query from the topic.
     - `write a blog about how to improve email open rates` → keyword: `how to improve email open rates`
2. Run /serp-gap-analysis with that query — **Phase 1 only** (winnability assessment). Do NOT proceed to Phase 2 (deep content gap analysis).
3. Check if the search intent and SERP from Phase 1 is related to the topic
   - If related → use this query
   - If not related → try a different query formulation
4. After 3 failed attempts → stop and report: "This may not be a good content idea (no matching searches)"
5. For the determined keyword, run /serp-gap-analysis Phase 2 (deep content gap analysis). Save the output to `{PROJECT_ROOT}/blogs/<topic>/gap-analysis.md`
