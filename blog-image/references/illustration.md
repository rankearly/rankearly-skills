# Illustration Mode Spec

- **Aspect:** Always use a horizontal canvas. Fit the width and height to the content's real size while keeping the frame landscape, with even padding around the full composition. Do not use a vertical canvas. Only force a specific ratio if the user explicitly asks for one.
- **Visual style:** Pure white background, clean documentation-diagram aesthetic, crisp vector lines, rounded shapes, airy spacing, subtle elevation, and restrained color. Avoid decorative gradients, muddy blur, or photographic texture.
- **What to specify:** Focus the prompt on four things: (1) the structure — how elements are arranged, (2) the exact labels inside each element, (3) the relationships — which elements connect to which and which items group together, (4) the colors that carry meaning. Skip pixel values, stroke weights, percentages, opacity numbers, and coordinate math — image models ignore them and they crowd out what matters.
- **Layout:** Choose the composition that best matches the concept. Use a pipeline only for genuinely sequential ideas; otherwise prefer simpler shapes like hub-and-spoke, grouped containers, loops, or split comparisons.
- **Composition:** Center the diagram with even padding and let the canvas fit the content. Keep connector flow clean and uncrossed. Use color or fill for emphasis instead of dramatic size jumps or effects.
- **Reusable units:** When a card, pill, or grouped stack repeats, define its internal structure and geometry explicitly. If those units should feel harmonious, require the same shape language, corner-radius family, inset, width logic, and spacing rhythm across all instances.
- **Hierarchy:** State which element should be visually dominant and which should stay quiet. Relative prominence is usually more important than extra styling adjectives.
- **Examples must be factually faithful to the concept being illustrated.** Before finalizing the prompt, ask: "If this diagram were real, would these specific examples actually behave this way?" Wrong examples teach the wrong mental model and undermine the diagram. If you don't know the domain well enough to pick accurate examples, ask the user.
- **Labels:** Keep captions minimal. Labels should name parts of the diagram, not explain the whole idea in prose.
- **Avoids:** Include a short avoid list for the most likely failure modes, especially mixed geometry, wrong grouping logic, copied reference layouts, or noisy connector routing.
- **Examples:** Use the short summaries below for pattern selection. Read `assets/cluster-related-keywords.md` or `assets/organize-clusters-into-topics.md` only if you need the full example prompt.

## Example

**User:** "Create an illustration for the 'Cluster related keywords' step: RankEarly compares the SERPs for keywords in that library and groups together keywords whose search results materially overlap. That forms your keyword clusters. The label for each keyword cluster comes from the highest-volume keyword inside that cluster."

Use a three-stage pipeline because this concept is truly sequential: keyword inputs -> SERP evidence -> resulting clusters. Keep repeated groupings visually aligned, show the middle SERP evidence as the reason for grouping, and use header fill to mark the lead keyword in each cluster. Full prompt: `assets/cluster-related-keywords.md`

## Example

**User:** "Generate the image prompt for the step 'Organize clusters into topics': RankEarly uses an NLP algorithm to group related keyword clusters into broader topics. This step is conservative by design: it prefers leaving weak matches separate instead of forcing them into the same topic."

Use a central-engine composition: keyword clusters flow into a compact NLP grouping engine and emerge as topic groups on the other side. Keep the engine secondary to the flow itself, and use one clean grouped connector per topic container. Treat the reference only as directional inspiration, not something to replicate. Full prompt: `assets/organize-clusters-into-topics.md`
