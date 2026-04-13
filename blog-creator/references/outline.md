# Outline Creator (Subagent)

Build a section-by-section outline for the blog post using the research gathered in earlier steps.

## What You Receive

- A subject to focus on.
- A keyword that matches the subject.
- `./blogs/<topic>/knowledge-base.md` — collected knowledge from SERP pages of the keyword
- `./blogs/<topic>/under-discussed.md` — questions competitors don't answer well

## Core Idea

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

## Storytelling Flow

Think hard about the order. The outline should read as a narrative, not a list of loosely related tips.

- **Adjacent sections must connect.** Each section should set up or follow from the one before it. If two sections feel unrelated sitting next to each other, something is wrong — reorder, merge, or cut.
- **Match section weight to insight depth.** If a point has real substance and changes how the reader thinks, give it space. If a point is thin — a single insight without much to unpack — keep it brief or fold it into a parent section. Do not create a wordy h2 for a thin point.
- **Some h2s are standalone, some need h3s.** A section with one clear idea needs no sub-sections. A section covering multiple related decisions benefits from h3s. Let the content decide the structure.
- **Cut what isn't worth explaining.** Not every insight from the research deserves a section. If it's trivia, tangential, or only interesting as a footnote, leave it out. A tighter article with fewer strong sections beats a comprehensive one full of filler.

## Adapt Based On

- **Conversion hooks** — place them where they serve the reader (e.g., a product capability as a concrete example in the framework section, a free tier mention in the next-step conclusion). Mark these placements in the outline with `[hook: ...]`.

## Output Format

Write to `./blogs/<topic>/outline.md` using the template at `assets/outline-template.md`.

Some h2s stand alone with no h3s. Others have multiple h3s — use h3s when the section covers several distinct perspectives, steps or sub-concepts that benefit from separation. Section word counts should roughly add up to the target.
