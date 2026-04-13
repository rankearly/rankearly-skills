# Outline Creator (Subagent)

Build a section-by-section outline for the blog post using the research gathered in earlier steps.

## What You Receive

- An idea of what to write.
- A keyword that matches the topic, and its related search intent, SERP (title + snippet).
- `./blogs/<topic>/knowledge-base.md` — collected knowledge from SERP pages of the keyword
- `./blogs/<topic>/under-discussed.md` — questions competitors don't answer well
- `./blogs/<topic>/gap-analysis.md` — competitive SERP gap analysis

## Process

1. **Pick the content format.**
   Read the recommended content format from `./blogs/<topic>/gap-analysis.md`. If the user has specified a different content format, use theirs instead.

2. **Load the matching format template.**
   Select the corresponding template from `assets/`. Use exactly one — do not mix templates.

   | Format | Template file |
   |--------|---------------|
   | Pillar page / ultimate guide | `assets/pillar-page.md` |
   | How-to guide | `assets/how-to-guide.md` |
   | Comparison | `assets/comparison.md` |
   | Case study | `assets/case-study.md` |
   | Benchmark / original research | `assets/benchmark-research.md` |
   | Interview / expert roundup | `assets/interview-roundup.md` |
   | News analysis | `assets/news-analysis.md` |
   | Listicle | `assets/listicle.md` |
   | FAQ / Q&A | `assets/faq.md` |
   | Glossary / definition | `assets/glossary-definition.md` |
   | Template / checklist | `assets/template-checklist.md` |

   Each template has **Bones** (required sections) and **Moves** (optional sections to pick from). Include all Bones. Pick 1-4 Moves based on what the topic actually needs — read the template's guidance and anti-patterns to decide. Don't include a Move just because it exists.

3. **Build the outline from the template.**
   Start with the Bones, then add the Moves you selected. For each section, write a 1-3 sentence description of what it covers and the key point it makes, following the format in `assets/outline-template.md`. Name sections after the actual content — not the template's generic labels. Every section must be grounded in the content topic and informed by the research files.

4. **Ensure the outline is centered around the content topic.**
   Every section — title, descriptions, examples — should tie back to the topic and keyword. Remove or rework anything generic that could belong to any article.

5. **Add conversion hooks.**
   Follow `references/conversion.md` to identify natural product mentions and write them to `{PROJECT_ROOT}/blogs/<topic>/conversion-hooks.md`. Then weave them into the outline, marked with `[hook: ...]`.

6. **Audit and polish.**
   Run the audit process described in `references/audit.md` on this first draft. Then revise the outline based on the review — reorder, merge, cut, or expand sections as needed — and produce the final version.

## Output Format

Write to `{PROJECT_ROOT}/blogs/<topic>/outline.md` using the template at `assets/outline-template.md`.

Some h2s stand alone with no h3s. Others have multiple h3s — use h3s when the section covers several distinct perspectives, steps or sub-concepts that benefit from separation. Section word counts should roughly add up to the target.
