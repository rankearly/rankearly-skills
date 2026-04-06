---
name: serp-gap-analysis
description: Analyze a live Google SERP for keyword winnability, competitor gaps, and SEO content brief creation. Use when the user asks for SERP analysis, real-result keyword difficulty, SEO competitor analysis, content gap analysis, or a brief or content plan for a specific keyword or query.
allowed-tools: list_keyword_libaries create_keyword_library add_or_update_keyword get_keyword analyze_serp get_research_status AskUserQuestion
metadata:
  displayName: SERP Gap Analysis
  status: live
  phases:
    - name: Collect input and resolve keyword library
    - name: Quick winnability assessment
    - name: Deep content gap analysis
---

# SERP Gap Analysis

Evaluate whether a keyword is realistically worth pursuing, then turn the live SERP into a compact brief that explains what content is required to compete and where the opportunity exists.

The skill has three required phases. Each phase has a corresponding output template in `templates/`.

## Phase 0: Collect Input and Resolve Keyword Library

Resolve the keyword library, then fetch fresh SERP data for the keyword.

Read `references/input-and-library.md` for the full process.

**Result**: a saved keyword record with top-10 SERP data and keyword metrics ready for Phase 1.

## Phase 1: Quick Winnability Assessment (subagent)

Determine whether the SERP is worth pursuing before investing in deeper analysis.

Read `references/winnability-rubric.md` for the verdict criteria, signal definitions, and scoring rules.

Use the keyword record from Phase 0 — the saved top-10 SERP titles, snippets, URLs, positions, plus keyword-level metrics (search volume, keyword difficulty, search intent, competition level).

**Deliverables**:
- Winnability verdict: `Winnable`, `Challenging`, or `Hard-to-Win`
- Search intent brief: 1 sentence
- Key signals summary: 3-5 bullets
- Recommendation: continue to Phase 2 or skip with reasoning

**Output**: use template from `templates/phase-1-winnability.md`.

## Phase 2: Deep Content Gap Analysis (subagent)

Analyze competitor weaknesses and define content requirements from the top 10 ranking pages.

Read `references/content-gap-process.md` for the async workflow and analysis approach.

**Workflow summary**:
1. `analyze_serp(kw, keyword_library, mode: "content_gap_analysis")` to start async analysis
2. Poll `get_research_status(task_id)` until complete
3. Present the consolidated result — `analyze_serp` already handles the full analysis internally

**Deliverables**:
- Must-have topics (table stakes)
- Target length range and content format recommendation
- Weakness analysis

**Output**: use template from `templates/phase-2-content-gap.md`.

After presenting Phase 2, ask whether the user wants to continue to create a blog post. If yes, hand off to the `blog-creator` skill with the content requirements gathered in this phase. The blog-creator skill will handle information gain research, outline creation, and full blog writing.
