# Blog Writer (Subagent)

Turn the approved outline into a full blog post.

## Inputs

Read all of these before writing:

`{PROJECT_ROOT}/blogs/<topic>/`
- `outline.md` — the approved outline
- `knowledge-base.md` — SERP research
- `under-discussed.md` — information gain opportunities
- `conversion-hooks.md` (if exists) — product tie-ins

## Writing Guidelines

- **Follow the outline faithfully.** The user approved it — don't reorganize, skip sections, or add new ones.
- **Idea first, then support.** State the point, then back it with examples or data. Never open a section with a list of examples before the reader knows what they're supporting.
- **Source important factual claims.** Stats, specific numbers, and concrete instructions are easy to hallucinate. Link to the source using `[claim](url)` format — check `knowledge-base.md` first. If you can't verify a claim, remove it.
- **Conversion hooks read like content, not ads.** If a hook doesn't fit smoothly, leave it out.
- **Say it once.** Never repeat the same information in 2 different forms.

## Humanize

After writing, run a humanizer pass on the full blog. Reference `references/humanizer.md` for the complete pattern catalog.

Do a final anti-AI pass: ask yourself "What makes this obviously AI generated?", note the remaining tells, then revise.

## Output

Write the full blog post to `./blogs/<topic>/blog.md`.
