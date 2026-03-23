# SERP Mode

Fetches live Google top 10 through RankEarly, analyzes competitor titles, then generates titles grounded in what's actually ranking.

This mode requires authenticating RankEarly MCP and consumes RankEarly credits.

## Step 0: Resolve the Keywords for SERP Analysis

- If the user already gave target keywords, confirm and use them directly
- If the user gave a content idea or draft description, extract 3 candidate target keywords that people would realistically search to find this blog, then ask (`AskUserQuestion`) the user to choose any that fit or add more keywords
- Only continue once the keyword list is confirmed
- Tell the user clearly that this mode uses RankEarly MCP and spends RankEarly credits

## Step 1: Fetch Live SERP Data

Call `scrape_serp` for each confirmed keyword to pull the top 10 Google results.

```
scrape_serp(query: "<keyword 1>")
scrape_serp(query: "<keyword 2>")
...
```

Extract from each result:
- Title (the actual title tag displayed in SERPs)
- URL (domain only for display)
- Position (1-10)
- Snippet

## Step 2: Analyze SERP Patterns

Analyze the top 10 competing titles for each keyword across these dimensions:

| Dimension | What to look for |
|-----------|-----------------|
| **Format distribution** | Count how many are how-tos, listicles, questions, comparisons, guides, other |
| **Common terms** | Words/phrases appearing in 3+ titles — these are terms Google is rewarding |
| **Title length** | Mean and range of character lengths |
| **Keyword placement** | How many front-load the keyword (first 3 words) vs. mid-place or bury it |
| **Gaps and opportunities** | Formats, angles, or modifiers that NO competitor uses (e.g., no listicles = differentiation opportunity; no year tag = freshness signal is open) |

Identify 2-3 explicit opportunity callouts.

## Step 3: Generate 10 Title Variations

Generate 10 titles informed by the SERP analysis, the chosen keywords, and the format preference.

Read `references/title-formulas.md` for the title-generation rules and real-world high-performing title patterns. Use as inspiration, not templates.

### Mode-specific guidance

- In **mix format**, weight toward formats underrepresented across the chosen SERPs (the gaps from Step 2)
- Incorporate relevant common terms from Step 2 where natural
- At least 2 titles should exploit a gap/opportunity from Step 2

## SERP-Specific Output

Before the per-title output (defined in SKILL.md), present the SERP pattern analysis for each confirmed keyword:

```
## SERP Pattern Analysis: [keyword]

**Top 10 Competing Titles:**
1. [Title] — [domain] (XX chars)
2. [Title] — [domain] (XX chars)
...
10. [Title] — [domain] (XX chars)

**Format Distribution:** X how-to, X listicle, X question, X guide, X other
**Common Terms:** [term1] (appears in X/10), [term2] (X/10), ...
**Average Title Length:** XX chars (range: XX-XX)
**Keyword Placement:** X/10 front-load the keyword

**Opportunities:**
- [Gap 1]
- [Gap 2]
- [Gap 3]
```

In the Recommendations section, also highlight which title best exploits a SERP gap.
