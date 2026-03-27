# SERP Mode

Uses a saved keyword record from the keyword library, analyzes the stored top 10 SERP titles, then generates titles grounded in what is already ranking.

This mode requires authenticating RankEarly MCP and consumes RankEarly credits.

## Step 0: Validate the Input

Confirm that blog context is already available, then require one target keyword for SERP mode.

- If the user provides blog context but no keyword, ask which keyword they want to target
- If the user provides multiple keywords, ask them to choose one primary keyword
- Tell the user clearly that this mode uses RankEarly MCP and may consume RankEarly credits if the keyword needs to be added to the library

Do not infer the keyword in SERP mode. Only continue once it is confirmed.

## Step 1: Resolve the Keyword Library

Read `./references/keyword-library-resolution.md` and resolve `keyword_library`.

## Step 2: Get the Keyword Record

Check whether the confirmed keyword already exists in the resolved library.

1. Call `get_keyword(kw, keyword_library)`.
2. If the keyword exists, use that saved keyword record and continue.
3. If the keyword does not exist, ask for explicit permission before adding it:

   ```text
   This keyword is not in the resolved keyword library. Do I have your permission to add it to the library first?
   ```

4. Only if the user explicitly grants permission, call `add_or_update_keyword(kw, keyword_library)`.
5. After adding, call `get_keyword(kw, keyword_library)` again and use the saved record.
6. If the user does not grant permission, stop and tell them SERP mode can only continue with a keyword that already exists in the resolved library.

Do not call `add_or_update_keyword` without explicit user permission when the keyword is missing.

The keyword record should contain:
- Keyword metrics such as search volume, keyword difficulty, intent, competition, and CPC when available
- Top-10 SERP snapshot with titles, snippets, URLs, and positions

## Step 3: Analyze SERP Patterns

Analyze the top 10 competing titles for the single confirmed keyword across these dimensions, while keeping the user's actual blog context in mind:

| Dimension | What to look for |
|-----------|-----------------|
| **Format distribution** | Count how many are how-tos, listicles, questions, comparisons, guides, other |
| **Common terms** | Words or phrases appearing in 3+ titles |
| **Title length** | Mean and range of character lengths |
| **Keyword placement** | How many front-load the keyword vs. mid-place or bury it |
| **Gaps and opportunities** | Formats, angles, or modifiers that no competitor uses |

Identify 2-3 explicit opportunity callouts.

## Step 4: Generate 10 Title Variations

Generate 10 titles informed by the user's blog context, the confirmed keyword, the SERP analysis, and the format preference.

Read `references/title-formulas.md` for the title-generation rules and real-world high-performing title patterns. Use them as inspiration, not templates.

Mode-specific guidance:
- In `mix` format, weight toward formats underrepresented in the saved SERP snapshot
- Incorporate relevant common terms where natural
- At least 2 titles should exploit a gap from Step 3
- Keep the angles aligned with the user's actual planned blog, not just the keyword

## SERP-Specific Output

Before listing the 10 title variations, present:

```markdown
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
