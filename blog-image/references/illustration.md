# Illustration Mode Spec

- **Aspect:** Always use a horizontal canvas. Fit the width and height to the content's real size while keeping the frame landscape, with even padding around the full composition. Do not use a vertical canvas. Only force a specific ratio if the user explicitly asks for one.
- **Background:** Pure white
- **Style:** Clean documentation diagram with a polished editorial illustration feel — precision vector, airy spacing, rounded shapes, subtle elevation, crisp anti-aliased edges, sharp vector lines, no muddy blur or photographic texture
- **Palette:** White background. Use only as many colors as the diagram needs; keep them harmonious. Avoid decorative gradients.
- **What to specify:** Focus the prompt on four things: (1) the structure — how elements are arranged, (2) the exact labels inside each element, (3) the relationships — which elements connect to which and which items group together, (4) the colors that carry meaning. Skip pixel values, stroke weights, percentages, opacity numbers, and coordinate math — image models ignore them and they crowd out what matters.
- **Framing:** Center the diagram on the canvas with clean, even padding. The frame should feel snug around the content without turning cramped. If the diagram is short, use less height. If it is narrow, reduce width only as long as the canvas remains clearly horizontal. Do not stretch the canvas just to satisfy a default ratio, and do not switch to portrait.
- **Flow:** Arrange groups so connection lines flow cleanly left-to-right (or top-to-bottom) in parallel, never crossing. Order items on each side so same-colored lines stay together.
- **Emphasis:** If one element needs emphasis, use color or fill — not size jumps, shadows, or glows.
- **Examples must be factually faithful to the concept being illustrated.** Before finalizing the prompt, ask: "If this diagram were real, would these specific examples actually behave this way?" Wrong examples teach the wrong mental model and undermine the diagram. If you don't know the domain well enough to pick accurate examples, ask the user.
- **Keep captions minimal.** Small labels that name a zone or mark a key transition are fine. What to avoid is verbose explanation — captions that restate the rule, describe what's happening, or narrate the diagram. Let the visual structure carry most of the meaning; captions should label, not explain.

## Example

**User:** "Create an illustration for the 'Cluster related keywords' step: RankEarly compares the SERPs for keywords in that library and groups together keywords whose search results materially overlap. That forms your keyword clusters. The label for each keyword cluster comes from the highest-volume keyword inside that cluster."

````
Elegant editorial-style documentation illustration on a pure white background. Landscape canvas sized to the actual footprint of the diagram with balanced padding on all sides, centered composition, no forced ratio beyond staying horizontal. Clean vector rendering, crisp anti-aliased lines, Inter / SF Pro style sans-serif, dark charcoal text, very light gray dividers, soft shadows, and restrained color accents in blue, teal, and warm orange.

Layout: one refined three-column composition with three small headings across the top: "Keywords" on the left, "SERP-based clustering" in the center, and "Keyword clusters" on the right. Add two faint vertical divider lines separating the three columns. Within that structure, show three horizontal groupings stacked with generous vertical spacing. No outer frame, no dense diagram scaffolding, no extra captions beyond what is necessary.

LEFT COLUMN — keyword inputs:
- Each grouping contains three softly tinted rounded keyword pills stacked vertically with even spacing, generous horizontal padding, and dark text.
- Group 1 uses a pale blue tint. Exact labels from top to bottom:
  1. email marketing ideas
  2. email marketing tips
  3. email marketing examples
- Group 2 uses a pale teal tint. Exact labels from top to bottom:
  1. welcome email examples
  2. welcome email templates
  3. welcome email sequence
- Group 3 uses a pale warm orange tint. Exact labels from top to bottom:
  1. abandoned cart email
  2. abandoned cart email examples
  3. abandoned cart email sequence
- These pills should feel light, airy, and elegant, not heavy badges. Use very soft tint fills, delicate borders, and subtle shadow only if needed to separate them from the background.

CENTER COLUMN — SERP evidence:
- For each grouping, place the label "Similar SERPs" above a pair of small search-result cards.
- Each pair contains exactly two miniature white SERP cards sitting side by side with tiny rounded corners, light gray borders, and a soft, tidy shadow.
- The cards are simplified result mockups, not readable full pages: one blue top bar, a few short gray text lines, and one or two small accent bars in that group's color.
- Group 1 accents are blue, group 2 accents are teal, group 3 accents are warm orange.
- Keep the SERP cards visually consistent across all three groups so the middle column reads as one repeated operation.

RIGHT COLUMN — resulting clusters:
- For each grouping, show one softly tinted rounded cluster container aligned with the corresponding keyword group and SERP pair.
- Inside each container, place one colored header pill at the top for the cluster label, then two lighter child pills beneath it.
- Group 1 cluster container uses pale blue with a blue header pill labeled "email marketing ideas". Beneath it, two light neutral pills read "email marketing tips" and "email marketing examples".
- Group 2 cluster container uses pale teal with a teal header pill labeled "welcome email examples". Beneath it, two light neutral pills read "welcome email templates" and "welcome email sequence".
- Group 3 cluster container uses pale warm orange with a warm orange header pill labeled "abandoned cart email". Beneath it, two light neutral pills read "abandoned cart email examples" and "abandoned cart email sequence".
- The colored header pill represents the highest-volume keyword in that cluster. Make it visually distinct through fill color only, not larger size or heavy decoration.

Relationships:
- Each keyword grouping connects to its matching SERP pair with one clean horizontal arrow in the same family color.
- Each SERP pair connects to its matching cluster container with one clean horizontal arrow in the same family color.
- The arrows are simple and elegant: medium weight, slightly softened edges, no dramatic glow, no tangled paths, no crossings.
- The reading order should be immediately obvious from left to right: keywords, similar SERPs, resulting cluster.
- Do not draw direct lines from individual keywords to individual cluster pills. The middle SERP evidence is the reason the keywords are grouped.

Style:
- Prioritize softness, balance, and restraint over hard-edged schematic precision.
- Use generous whitespace, calm vertical rhythm, centered overall composition, and consistent rounded geometry.
- Keep typography light and readable, not bold everywhere.
- Use tinted containers and subtle elevation to create hierarchy instead of heavy outlines or bright fills.
- No icons, no busy annotations, no gradients used as decoration, no dark background blocks, no clutter.
````
