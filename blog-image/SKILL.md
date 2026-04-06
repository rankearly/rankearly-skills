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

Generate **one optimized Nanobanana Pro prompt** for a blog image based on the user's request.

## Step 1: Determine Mode

| Mode | When to use | Focus |
|------|-------------|-------|
| **Cover** | Header image, hero image, "cover", "thumbnail", scroll-stopper | Visual impact, abstract, attention-grabbing |
| **Illustration** | In-post diagram, workflow comparison, "explain", "show", concept visualization | Clarity, literal representation, educational |

## Step 2: Mode-Specific Settings

### Cover
- **Background:** Dark navy/charcoal with subtle vignette
- **Aspect:** 3:2
- **Style:** Premium SaaS / editorial tech poster, abstract visual impact
- **Rules:** No logos, no watermarks. If no title requested: no text, no letters/numbers.
- **Title overlay (optional):** When user provides a blog title, incorporate it into the composition:
  - Place title text dead center, occupying roughly 50% of the image height — dominant and unmissable
  - Use bold, clean sans-serif typography (Inter, SF Pro style)
  - White or near-white text with subtle shadow/glow for readability
  - Abstract elements stay minimal and behind the title, never competing with it
- **Palette:**
  - Primary: Trusty Blue `#2563EB`
  - Accent: warm orange `#F97316`
  - Neutrals: slate/steel grays, deep navy/charcoal

### Illustration
- **Background:** White or very light neutral (`#FAFAFA` or `#F8F9FA`)
- **Aspect:** 3:2 (or as needed)
- **Style:** Modern SaaS, precision vector, Think Linear/Notion/Vercel. Rendered at high detail with crisp anti-aliased edges.
- **Rules:** Clear visual hierarchy, can include diagrams/flowcharts. Each image focuses on one specific concept — no multi-topic compositions. Use precise geometric shapes with consistent stroke weights (2px). Limit to 3–4 colors per image for clarity.
- **Palette:** Brand colors for emphasis, neutral grays for structure. Avoid gradients unless they convey meaning (e.g., progression).
- **Quality directives:** Sharp vector edges, no blur or soft-focus effects, legible labels at 1x resolution, generous whitespace between elements.

## Step 3: Generate Prompt

Use this structure for all modes:

```
**Mode:** [Cover / Illustration]

**Focus:** [One-line description of the visual's purpose]

---

> [ASPECT RATIO] [TYPE], [STYLE DESCRIPTORS]. [BACKGROUND DESCRIPTION].
>
> [LAYOUT - describe the visual structure]
>
> [ELEMENT A - detailed description with colors, positioning, visual cues]
>
> [ELEMENT B - detailed description with colors, positioning, visual cues]
>
> [ADDITIONAL ELEMENTS if needed]
>
> [STYLE NOTES specific to this mode]
>
> [KEY VISUAL CONTRASTS OR HIERARCHY TO EMPHASIZE]

**Params:**
- Aspect ratio: [ratio]
- Style: [style notes]
- Quality: high detail, sharp vector edges, crisp anti-aliased lines
```

## Examples

### Cover Example (no title)

**User:** "Generate a blog cover for my post about keyword clustering"

**Mode:** Cover

**Focus:** Abstract visual suggesting grouping/organization, scroll-stopping

---

> 3:2 blog cover, ultra-clean premium SaaS aesthetic. Dark navy/charcoal background with subtle vignette. A single large glowing portal ring off-center, with layered concentric arcs and light streaks swirling into the ring — suggesting aggregation and clustering. Strong contrast: Trusty Blue #2563EB as primary glow, warm orange #F97316 as accent highlights, with slate/steel grays for structure. Tasteful soft bloom, faint film grain, tiny bokeh particles, crisp edges, minimal clutter, modern tech poster style, high-end lighting, no text, no logos.

### Cover Example (with title)

**User:** "Generate a blog cover for my post about keyword clustering, title: 'Keyword Clustering: The Complete Guide'"

**Mode:** Cover (titled)

**Focus:** Abstract clustering visual with prominent title text overlay

---

> 3:2 blog cover, ultra-clean premium SaaS aesthetic. Dark navy/charcoal background with subtle vignette. The text "Keyword Clustering: The Complete Guide" displayed dead center in bold white sans-serif typeface with a subtle blue glow shadow. Layered concentric arcs and light streaks swirling into a glowing ring around and behind the title — suggesting aggregation and clustering. Strong contrast: Trusty Blue #2563EB as primary glow, warm orange #F97316 as accent highlights, with slate/steel grays for structure. The typography is crisp and readable, abstract elements frame the text without competing. Tasteful soft bloom, faint film grain, modern tech poster style, high-end lighting.

**Params:**
- Aspect ratio: 3:2
- Style: Premium SaaS, dark theme, abstract
- Quality: high detail, sharp edges

### Illustration Example

**User:** "Create an illustration showing top-down vs bottom-up content strategy workflows"

**Mode:** Illustration

**Focus:** Comparing two content strategy approaches with directional contrast

---

> 3:2 infographic, modern SaaS illustration style, clean vector aesthetic. White background.
>
> **LEFT COLUMN - "Traditional Manual Approach" (Top-Down):**
> - Frustrated marketer at top with lightbulb, manually guessing pillar topics
> - Arrows pointing DOWN to pre-defined content pillar boxes
> - Below that, more arrows DOWN to keyword lists forced into pillars
> - Bottom: disconnected content pieces mismatching search intent
> - Muted gray-ish blue tones, visual friction cues (question marks, crossed-out items)
> - Label: "Start with assumptions, force keywords into pillars"
>
> **RIGHT COLUMN - "Data-Driven Workflow" (Bottom-Up):**
> - Clean interface at BOTTOM with raw keyword data flowing IN
> - Arrows pointing UP as SERP data groups keywords into clusters
> - Clusters merge and consolidate into revealed pillar topics
> - Top: confident marketer with clear, validated content strategy
> - Vibrant teal/green accents, clarity cues (checkmarks, connected nodes)
> - Label: "Start with data, let pillars emerge from search reality"
>
> **Key contrasts:** Direction (down vs up), Emotion (frustration vs confidence), Outcome (mismatch vs alignment)

**Params:**
- Aspect ratio: 3:2
- Style: Modern SaaS, precision vector, minimal gradients
- Quality: high detail, sharp vector edges, crisp anti-aliased lines, legible labels

