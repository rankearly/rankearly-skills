---
name: blog-image
description: Generate a Nanobanana Pro prompt for blog images - either a scroll-stopping cover or an explanatory in-post illustration. Use when the user asks for a "blog cover", "blog image", "post thumbnail", "illustration for my blog", "header image", or wants to create a visual for a blog post or article section.
metadata:
  displayName: Blog Image
  status: live
  phases:
    - name: Determine mode
    - name: Generate prompt
---

Generate **one optimized Nanobanana Pro prompt** for a blog image.

## Step 1: Pick the mode

| Mode | Use when the user wants... | Goal |
|------|---------------------------|------|
| **Cover** | A header, hero, thumbnail, or scroll-stopper | Visual impact — abstract and attention-grabbing |
| **Illustration** | An in-post diagram, workflow, comparison, or concept explainer | Clarity — literal and educational |

If the user supplies a blog title for a cover, treat it as a **titled cover** (title becomes the focal point).

## Step 2: Apply the mode spec

### Cover spec

- **Aspect:** 3:2
- **Background:** Dark navy/charcoal with subtle vignette
- **Style:** Premium SaaS / editorial tech poster, abstract, high-end lighting
- **Palette:**
  - Primary: Trusty Blue `#2563EB`
  - Accent: warm orange `#F97316`
  - Neutrals: slate/steel grays, deep navy/charcoal
- **Rules:** No logos, no watermarks. If no title is provided, include no text at all.
- **Titled covers:** Place the title text dead center, roughly 50% of image height, in bold clean sans-serif (Inter / SF Pro style), white with a subtle glow or shadow for readability. Abstract elements sit behind the title and never compete with it.

### Illustration spec

- **Aspect:** 3:2 (unless the concept needs otherwise)
- **Background:** Pure white
- **Style:** Clean documentation diagram — precision vector, polished SaaS aesthetic, crisp anti-aliased edges, sharp vector lines, no blur or soft focus
- **Palette:** White background. Use only as many colors as the diagram needs; keep them harmonious. Avoid decorative gradients.
- **Composition rules:**
  - Center the canvas and center major element groups
  - Few elements, few connection lines, no tangled paths
  - One consistent UI language across pills, cards, arrows, and containers
  - Generous whitespace, balanced alignment, consistent stroke weights
  - No nested diagram containers unless the user explicitly asks for panels
- **Emphasis rules:** If one element needs emphasis, use color or fill — not size jumps, shadows, glows, or extra decoration. Stay restrained, not fancy.
- **Labeling:** Use exact text labels inside the diagram whenever the meaning depends on the label. When writing the prompt, always specify: the row/column structure, the exact labels, which elements connect to which, which items are grouped, and which items are visually distinct and why.

## Step 3: Write the prompt

Use this structure:

```
**Mode:** [Cover / Illustration]

**Focus:** [One-line description of the visual's purpose]

---

> [ASPECT] [TYPE], [STYLE DESCRIPTORS]. [BACKGROUND].
>
> [LAYOUT — structure, placement, spacing]
>
> [ELEMENTS — each with color, position, label, visual cue]
>
> [RELATIONSHIPS — what connects, groups, or contrasts]
>
> [STYLE NOTES from the mode spec above]
```

Keep the prose tight. Every sentence should either describe something the generator needs to draw or a style rule it needs to follow.

## Examples

### Cover — no title

**User:** "Generate a blog cover for my post about keyword clustering"

**Mode:** Cover
**Focus:** Abstract visual suggesting grouping/organization, scroll-stopping

---

> 3:2 blog cover, ultra-clean premium SaaS aesthetic. Dark navy/charcoal background with subtle vignette. A single large glowing portal ring off-center, with layered concentric arcs and light streaks swirling into the ring — suggesting aggregation and clustering. Strong contrast: Trusty Blue #2563EB as primary glow, warm orange #F97316 as accent highlights, with slate/steel grays for structure. Tasteful soft bloom, faint film grain, tiny bokeh particles, crisp edges, minimal clutter, modern tech poster style, high-end lighting. No text, no letters or numbers, no logos, no watermarks.

### Cover — with title

**User:** "Generate a blog cover for my post about keyword clustering, title: 'Keyword Clustering: The Complete Guide'"

**Mode:** Cover (titled)
**Focus:** Abstract clustering visual with prominent title text overlay

---

> 3:2 blog cover, ultra-clean premium SaaS aesthetic. Dark navy/charcoal background with subtle vignette. The text "Keyword Clustering: The Complete Guide" displayed dead center in bold white sans-serif typeface (Inter / SF Pro style) with a subtle blue glow shadow, occupying roughly half the image height. Layered concentric arcs and light streaks swirl into a glowing ring around and behind the title — suggesting aggregation and clustering. Strong contrast: Trusty Blue #2563EB as primary glow, warm orange #F97316 as accent highlights, with slate/steel grays for structure. Typography is crisp and readable; abstract elements sit behind the title and never compete with it. Tasteful soft bloom, faint film grain, modern tech poster style, high-end lighting. No logos, no watermarks.

### Illustration

**User:** "Create an illustration showing top-down vs bottom-up content strategy workflows"

**Mode:** Illustration
**Focus:** Comparing two content strategy approaches with directional contrast

---

> 3:2 infographic, modern SaaS documentation illustration, clean vector aesthetic. Pure white background.
>
> **LEFT COLUMN — "Traditional Manual Approach" (Top-Down):**
> - One centered vertical flow
> - Marketer at top, then guessed topic boxes, then forced keyword lists, then mismatched content pieces
> - Straight downward arrows only
> - Muted gray-blue tones
> - Label: "Start with assumptions, force keywords into pillars"
>
> **RIGHT COLUMN — "Data-Driven Workflow" (Bottom-Up):**
> - One centered vertical flow
> - Raw keyword data at bottom, then grouped clusters, then revealed topics, then confident marketer at top
> - Straight upward arrows only
> - Teal accents for grouped data
> - Label: "Start with data, let pillars emerge from search reality"
>
> **Relationships:** Both columns are structurally mirrored for easy comparison. Text labels sit inside the diagram. Emphasis is carried only by color fill on the grouped clusters and final topics — no size jumps, shadows, or glows. No decorative elements, background panels, nested containers, or tangled arrows.
>
> **Style:** Pure white background, centered composition, polished documentation style, consistent shapes and stroke weights, generous whitespace, balanced spacing, restrained harmonious colors, no gradients, sharp vector edges, crisp anti-aliased lines, legible labels.
>
> **Key contrasts:** Direction (down vs up), Outcome (mismatch vs alignment).
