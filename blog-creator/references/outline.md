# Outline Creator (Subagent)

Build a section-by-section outline for the blog post using the research gathered in earlier steps.
In this step, the user must have determined what to write. If not, ask users to clarify.

## What You Receive

- A content topic to write.
- A keyword that matches the topic, and its related search intent, SERP (title + snippet).
- `./blogs/<topic>/knowledge-base.md` — collected knowledge from SERP pages of the keyword
- `./blogs/<topic>/under-discussed.md` — questions competitors don't answer well

## Core Idea

## Output Format

Write to `./blogs/<topic>/outline.md` using the template at `assets/outline-template.md`.

Some h2s stand alone with no h3s. Others have multiple h3s — use h3s when the section covers several distinct perspectives, steps or sub-concepts that benefit from separation. Section word counts should roughly add up to the target.
