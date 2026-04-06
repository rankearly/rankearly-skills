# Outline Creator (Subagent)

Build a section-by-section outline for the blog post using the research gathered in earlier steps.

## What You Receive

- `./blogs/<topic>/knowledge-base.md` — collected knowledge from SERP pages
- `./blogs/<topic>/under-discussed.md` — questions competitors don't answer well
- `./blogs/<topic>/conversion-hooks.md` (if exists) — product tie-ins that fit the topic
- Target word count (if specified)

## Outline Structure

Use this as a starting skeleton — adapt sections to the content format and topic:

1. **Hook** — grab attention, establish relevance
2. **Problem** — what's at stake, why it matters
3. **Why existing advice is incomplete** — set up your unique angle
4. **Your framework/method** — the core value
5. **Examples/applications** — make it concrete
6. **Mistakes/caveats** — build trust, add depth
7. **Conclusion/next step** — actionable takeaway

Not every article needs all seven. A tutorial might skip "why existing advice is incomplete." A comparison post might merge framework + examples. Use judgment.

## Adapt Based On

- **Word count** — expand or compress sections accordingly
- **Must-have topics** — verify knowledge base has content to cover each
- **Under-discussed questions** — integrate 2-3 as your information gain. These are the sections where you say something the top results don't — they're what make the article worth publishing.
- **Conversion hooks** — place them where they serve the reader (e.g., a product capability as a concrete example in the framework section, a free tier mention in the next-step conclusion). Mark these placements in the outline with `[hook: ...]`.

## Output Format

Write to `./blogs/<topic>/outline.md` using this format:

```
# {Article Title}

Target: ~{N} words

## {H2 Title}
{1-2 sentence description of what this section covers and the key point it makes}
(~{word count} words)

## {H2 Title}
{1-2 sentence description of what this section covers and the key point it makes}
(~{word count} words)

...
```

Repeat for each section. Section word counts should roughly add up to the target.
