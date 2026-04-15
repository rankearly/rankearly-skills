# Illustration Mode Spec

The caller provides a specific point to illustrate. Your job is to figure out the best angle and draw a clean diagram.

## Workflow

### 1. Find the angle

Don't try to visualize the full concept. Find one specific scenario, case, or example that makes the point land. The narrower the better.

- Bad: "show how market-first keyword research works across all markets"
- Good: "show that the same English word resolves to different terms in US vs UK — 'sneakers' vs 'trainers' — so one list can't serve both"

The angle should be something a reader can verify at a glance. If it requires reading labels for 30 seconds to understand, the angle is too broad.

### 2. Draw the diagram

Write a prompt that produces a simple, precise, detailed diagram. The prompt should specify:

1. **Structure** — how elements are arranged (a table, a flow, grouped boxes, a before/after split, etc.). Use whatever form fits the idea.
2. **Labels** — the exact text inside each element. Keep labels short. They name parts, not explain ideas.
3. **Relationships** — which elements connect, group, or contrast with which. Be explicit about what links to what.
4. **Color meaning** — if color carries information (e.g., blue = shared, orange = different), state it. Use 2-3 colors max.

## Prompt rules

- **White background, flat clean style, horizontal canvas.** This is non-negotiable — image-gen models handle this reliably.
- **Keep the total element count low.** 3-8 distinct visual elements is the sweet spot. More than that and the model loses coherence.
- **Specify concrete examples, not abstract placeholders.** "Sneakers" and "Trainers" teach more than "Term A" and "Term B".
- **No metaphors or decorative elements.** No plants, no icons representing abstract ideas, no visual flourishes. Show the actual data or structure.
- **No pixel values, opacity, stroke weights, coordinate math.** Image models ignore them. Describe spatial relationships in plain language (e.g., "side by side", "stacked vertically", "connected by a line").
- **Include a short avoid list** for likely failure modes: crossed lines, misaligned groups, photographic texture, vertical orientation.
- **Examples must be factually accurate.** If the diagram shows a specific keyword producing specific results, those relationships should be plausible. Wrong examples teach wrong mental models.

## Example

**User:** "Illustrate that same-language markets need separate keyword libraries"

**Angle:** Show that US-en and UK-en use different words for the same things, so a single English keyword list misses half the real search terms in each market.

**Prompt structure:** A simple two-column comparison table. Left column header: "US-en". Right column header: "UK-en". Three rows showing real term pairs: "sneakers / trainers", "checking account / current account", "cell phone plan / mobile tariff". Below the table, a single line of text: "Same language. Different search terms. Different libraries."

This works because the reader gets the point in under 3 seconds. No connecting lines, no multi-stage flows, no decorative elements. Just the evidence.
