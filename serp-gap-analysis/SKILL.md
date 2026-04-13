---
name: serp-gap-analysis
description: Analyze a live Google SERP for keyword winnability and competitor gaps. Use when the user asks for SERP analysis, real-result keyword difficulty, SEO competitor analysis, content gap analysis, or a brief or content plan for a specific keyword or query.
allowed-tools: list_keyword_libaries create_keyword_library add_or_update_keyword get_keyword analyze_serp AskUserQuestion
metadata:
  displayName: SERP Gap Analysis
  status: live
  phases:
    - name: Collect input and resolve keyword library
    - name: Quick winnability assessment
    - name: Deep content gap analysis
---

## Steps

0. **Collect input** (subagent) — Ref: `references/input-and-library.md`. Fetch fresh SERP data for the keyword and resolve the keyword library. Returns: saved keyword record with top-10 SERP + metrics.
1. **Winnability assessment** (subagent) — Ref: `references/winnability-rubric.md`. Uses keyword record from step 0. Output template: `templates/phase-1-winnability.md`. Returns: verdict (Winnable / Challenging / Hard-to-Win), search intent, key signals, recommendation to continue or skip.
2. **Content gap analysis** (subagent) — Call `analyze_serp(kw, keyword_library, mode: "content_gap_analysis")` and return the tool's markdown directly without reformatting. Returns: must-have topics, target length/format, weakness analysis.

After presenting Phase 2, suggest the user run `/blog-creator` to turn the SERP analysis into a full blog post.
