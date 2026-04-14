# Outline Audit (Subagent)

Score the outline against the criteria below. For each criterion, assign Pass / Partial / Fail with a one-line reason. End with an overall verdict (Accept / Revise) and a bullet list of concrete changes if Revise. Save the result to `{PROJECT_ROOT}/blogs/<topic>/audit.md`.

---

## Core Idea

- **C01 — Intent Alignment.** Title promise matches the sections that will deliver on it. Fail if the outline drifts from or under-delivers on the title.
- **C05 — Topic Scope.** Outline makes clear what is and is not covered. Fail if scope is unbounded or vague.
- **C06 — Audience Targeting.** Target reader is evident from depth and framing. Fail if difficulty level is inconsistent across sections.
- **C08 — Use Case Mapping.** Outline includes a decision framework or "when to use what" angle where the topic warrants it. Fail if the topic demands comparison but the outline doesn't frame choices.
- **E04 — Contrarian / Fresh Angle.** Outline has a clear point of view, not just a summary of consensus. Partial if it rehashes the standard take with minor additions.
- **E06 — Gap Filling.** Outline targets questions or angles competitors miss. Fail if every section maps 1:1 to existing top-ranking content.

## Structure & Flow

- **O01 — Heading Hierarchy.** Single H1; H2/H3 nesting is logical with no level skips.
- **O06 — Section Chunking.** Each section owns one clear topic. Fail if a section mixes unrelated ideas.
- **O09 — Information Density.** No filler sections. Every section earns its place with real substance. Fail if sections exist just to pad word count.
- **Flow.** Adjacent sections set up or follow from each other. If two sections feel unrelated side by side — reorder, merge, or cut.
- **Weight matches depth.** Space is proportional to substance. Thin points should fold into a parent section or be cut.
- **Structure follows content.** A section with one idea needs no h3s. A section covering multiple sub-concepts benefits from h3s.

## Conversion Hooks

- **Placement.** Hooks appear where they serve the reader (e.g. product capability as a concrete example, free-tier mention in the conclusion). Mark with `[hook: ...]`.
- **Restraint.** No more than 2–3 hooks per article. Fail if hooks interrupt the reader's train of thought.
