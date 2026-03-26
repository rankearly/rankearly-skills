---
name: serp-gap-analysis
description: Assess keyword winnability from a live Google SERP, find competitor content gaps, and generate an SEO content brief. Use when the user asks for SERP analysis, keyword difficulty with real results, SEO competitor analysis, content gap analysis, or a content plan for a specific keyword or query.
allowed-tools: list_keyword_libaries list_projects create_keyword_library add_or_update_keyword get_keyword analyze_serp get_research_status AskUserQuestion
metadata:
  displayName: SERP Gap Analysis
  status: live
  phases:
    - name: Collect input and resolve keyword library
    - name: Quick winnability assessment
    - name: Deep content gap analysis
    - name: Content brief with information gain (optional)
---

# SERP Gap Analysis

Evaluate whether a keyword is realistically worth pursuing, then turn the live SERP into a compact brief that explains what content is required to compete and where the opportunity exists.

The skill has two required phases. An optional Phase 3 runs only if the user explicitly opts in after Phase 2. Each phase has a corresponding output template in `templates/`.

## Phase 0: Collect Input and Resolve Keyword Library

Resolve the keyword, ask the user to choose from a library option list that includes existing libraries plus `New keyword library`, then fetch fresh SERP data.

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

After presenting Phase 2, end the reply with one natural question that does both:

- asks whether to continue and create a content brief with an outline of H2 - description sections
- asks what business, product, feature set, firsthand experience, or proprietary data the user can bring that competitors do not cover

Continue to Phase 3 only when the user explicitly says yes. Use the user's reply as the primary source of business or product context. End the skill after Phase 2 when the user declines.

## Phase 3: Content Brief with Information Gain and Outline

Only runs if the user explicitly says yes after Phase 2.

Read `references/information-gain.md` for how to collect and apply the user's unique context.

Use the context the user provides in response to the Phase 2 question before generating the brief. Build differentiation from the user's actual context. If they say yes but do not provide enough detail, ask one short follow-up about the missing business, product, feature, experience, or proprietary-data context.

**Deliverables**:
- Information gain analysis
- Angle recommendations
- Outline as H2 - description pairs

**Output**: use template from `templates/phase-3-content-brief.md`.
