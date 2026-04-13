# Image Illustrator

Generate illustration image prompts for sections of a finished blog post.

## Input

- The finished blog at `./blogs/<topic>/blog.md`

## Process

1. Read the blog and identify 1–3 sections where a targeted illustration would help the reader understand a specific point — a comparison, a workflow step, a before/after, or a mental model.

2. Do NOT illustrate the entire section. Zero in on the single most valuable idea within that section. For example: if a section covers "three ways to do X," pick the one way that benefits most from a visual, not all three.

3. For each selected point, run /blog-image in Illustration mode. Pass a focused description of the specific concept to illustrate.

4. Insert the generated prompt and an image placeholder into the blog file at the end of the corresponding section:

```
![descriptive alt text](images/filename.jpg)

<!-- blog-image
[paste the generated image-gen prompt here]
-->
```

## Guidelines

- **One concept per image** — keep it clean and focused, no visual clutter.
- **Prefer diagrams, comparisons, or workflows** over decorative visuals.
- **Skip sections that are self-explanatory** from the text alone.
- **Be selective** — not every blog needs 3 images. One great illustration beats three mediocre ones.
