---
name: blog-title-generator
description: Generate SEO blog titles, title tags, and H1 variations for a keyword or content idea. Use when the user wants blog title ideas, headline options, title tag suggestions, H1 variants, or SEO/CTR title optimization.
allowed-tools: scrape_serp
metadata:
  displayName: Blog Title Generator
  status: live
  phases:
    - name: Accept input
    - name: Choose mode (SERP-grounded or quick)
    - name: Generate 10 scored title variations
---

# Blog Title Generator

Generate 10 blog title variations, each with a title tag and H1, scored across 5 dimensions with a short explanation of why it works.

## Phase 0: Accept Input

The user provides either:
- A **target keyword** (short, query-like phrase) — use it directly in either mode
- A **content idea or draft description** — use it as the working topic. Only resolve it into a keyword if the user chooses SERP mode

Also accept an optional **format preference**: `how-to`, `listicle`, `question`, `comparison`, `ultimate-guide`, `curiosity`, or `mix` (default: `mix`).

Output: the captured input and format preference. Mode-specific handling lives in the reference files.

## Phase 1: Choose Mode

Ask the user (AskUserQuestion): **"Want live SERP-grounded titles first? That requires authenticating RankEarly MCP and consumes RankEarly credits. Or I can generate quick titles right away without RankEarly."**

- If the user wants SERP analysis → read `references/serp-mode.md` and follow it, then return here for Phase 2
- If the user wants quick titles → read `references/quick-mode.md` and follow it, then return here for Phase 2

## Phase 2: Score, Annotate, and Present

After generating 10 title variations (from either mode), apply the following to each title.

### Dual output per variation

For each of the 10 variations, produce:

- **Title Tag** — CTR-optimized for SERP display. Usually aim for 50-65 characters, but go longer when clarity wins. Front-load the primary phrase when possible.
- **H1** — Reader-optimized for on-page experience. No character cap. Can be more conversational, descriptive, or provocative.

In SERP mode, optimize each title around one of the confirmed keywords. In quick mode, optimize around the user's original topic or phrase.

### Score each title

Evaluate each title tag across 5 dimensions using qualitative labels (not numeric scores — labels are immediately actionable):

| Dimension | What to evaluate | Labels |
|-----------|-----------------|--------|
| **Primary Phrase Placement** | Is the chosen keyword for that title (SERP mode) or main topic phrase (quick mode) in the first 3 words? First half? Second half? | Front-loaded / Mid-placed / Buried |
| **Character Length** | Character count relative to the usual 50-65 char target range | Strong (50-65) / Acceptable (40-49 or 66-75) / Long (76+) |
| **Power Words** | Proven engagement words: definitive, proven, free, steal, easy, fast, etc. | Strong (2+) / Present (1) / None |
| **Specificity** | Numbers, percentages, timeframes, platform names, audience qualifiers | High / Moderate / Low |
| **Emotional Sentiment** | What emotion does the title trigger? | Positive / Negative / Neutral — plus the specific emotion (curiosity, fear, aspiration, urgency) |

Also show:
- Exact character count for the title tag
- Note when the title tag is longer than 65 characters

### Annotate each title

Add a 1-2 sentence annotation explaining the copywriting technique and why it works. Be specific about the effect; avoid generic comments like "uses a number and a power word."

### Per-title output format

```markdown
### Title [N]: [Format Type]

**Title Tag** (XX chars): [title tag version]
**H1**: [H1 version]

**Scores:**
- Primary Phrase Placement: [label]
- Character Length: [label] — XX chars
- Power Words: [label] — [list the power words]
- Specificity: [label] — [what elements]
- Sentiment: [label] — [specific emotion]

**Why this works:** [1-2 sentence annotation]
```

### Recommendations

Close with 3-5 sentences highlighting:
- Which 2-3 titles are strongest and why
- Any trade-offs the user should consider
