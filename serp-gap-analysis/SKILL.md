---
name: serp-gap-analysis
description: Assess whether a SERP is winnable based on competitive signals, then analyze weaknesses in ranking pages to surface content opportunities you can exploit.
allowed-tools: scrape_serp
metadata:
  displayName: SERP Gap Analysis
  status: live
  phases:
    - name: Fetch live Google top-10 results
    - name: Score SERP competitiveness
    - name: Audit each page for gaps
    - name: Surface actionable recommendations
---

# SERP Gap Analysis

Assess whether a SERP is winnable based on competitive signals, then analyze weaknesses in the ranking pages to surface content opportunities.

## Workflow

Four phases, run in order:

0. **SERP Fetch** — Retrieve live search results for the keyword
1. **Winnability Assessment** — Can this SERP realistically be won?
2. **Weak Spot Analysis** — Where exactly are the ranking pages falling short?
3. **Content Opportunities** — What should the user do about it?

## Phase 0: SERP Fetch

Before any analysis, call the `scrape_serp` MCP tool to retrieve live Google results:

```
scrape_serp(query: "<keyword>")
```

This returns the top-10 organic results with title, URL, snippet, position, and date. Use these results as the raw input for all subsequent phases. Do not ask the user to provide SERP data manually.

## Phase 1: Winnability Assessment

Assess winnability at the SERP snippet level using the results from Phase 0 — no need to fetch full page content yet. The goal is a quick triage so the user doesn't invest time diving deep into a hard-to-win SERP.

Score the SERP by checking for these signals:

**Positive signals** (suggest the SERP is beatable):
- Stale pages ranking high (last updated 6+ months ago)
- Low keyword difficulty (KD)
- Mixed results — small brands, forums, UGC, or low-authority domains hold at least 5 of the top 10 spots
- Results with mismatched search intent (e.g., informational page ranking for a transactional query)

**Negative signals** (suggest the SERP is hard to crack):
- High keyword difficulty (KD)
- Big brands or high-authority domains dominate at least 5 of the top 10 spots

**Verdict logic:**
- 2+ positive signals, 0 negative → **Winnable**
- 1+ negative signals → **Hard-to-win**
- Otherwise → **Challenging**

**What to do next:**
- **Winnable**: Summarize the search intent, then proceed to Phase 2.
- **Hard-to-win** / **Challenging**: Stop and ask the user whether they still want to see the weak spots before continuing. They may decide to target a different keyword instead.

## Phase 2: Weak Spot Analysis (parallel subagents)

Spawn one subagent per ranking page to analyze it independently. Parallel execution keeps this fast — each page analysis is self-contained.

**Subagent input:**
- Ranking position (1-10)
- Page URL
- Last updated date
- Search intent summary (from Phase 1)

**Subagent instructions — evaluate the page against these dimensions:**

| Dimension | What to look for |
|-----------|-----------------|
| **Answer sufficiency** | Does the page actually solve the searcher's intent? Does it answer the core question, or does it dance around it? |
| **Originality** | Does the content show original thinking — unique data, first-hand experience, original viewpoints? Or is it a rehash of other search results? |
| **Credibility** | Are sources cited? Is there a visible author with relevant expertise? Does the site show clear ownership and authority signals? |
| **Freshness** | Was the page updated in the last 6 months? Are the examples, data, and recommendations current? |
| **Readability** | Is the content easy to consume? Good structure, scannable headings, appropriate length? Or is it a wall of text? |

For each dimension where the page is weak, record a short explanation of the specific weakness (not just "weak on originality" — say what's actually missing).

**Subagent output:** Save results to `./serp-gap/{query}/{ranking-position}.json`:

```json
{
  "position": 3,
  "url": "https://example.com/page",
  "last_updated": "2024-08-15",
  "weak_spots": [
    {
      "dimension": "freshness",
      "detail": "Last updated 14 months ago. References 2023 pricing that has since changed."
    },
    {
      "dimension": "originality",
      "detail": "No original data or first-hand experience. Restates common advice found on every competitor page."
    }
  ]
}
```

## Phase 3: Content Opportunities

After all subagents complete, unify the weak spot data from `./serp-gap/{query}/` into a list of content opportunities — specific, actionable recommendations the user can act on.

Each opportunity should connect a recurring weakness across multiple ranking pages to a concrete action. For example, if 4 of the top 10 pages lack original data, the opportunity is "Include original benchmarks or case study data — most competitors rely on generic advice."

**Before generating opportunities, ask the user:**
- Do you already have an article targeting this keyword?
  - **Yes** → Run Weak Spot Analysis on their article too, then frame opportunities as improvements to their existing content.
  - **No** → Frame opportunities as requirements for a new article. Suggest using the `content-brief` skill as the next step.
