# SEO Memory Update Guide

Instructions for updating the seo-memory file. Used by subagents dispatched from the seo-memory skill.

## Read first

Read `./seo-memory.md` to understand the current state before making changes.

## Apply the update

Parse what the user shared and place it in the correct section.

See `template.md` for section definitions and entry formats. For offerings, connect each capability to a clear customer benefit. Prefer customer-facing language over internal implementation details.

**Deduplication rules:**
- If an existing entry covers the same topic, update it in place — don't create a duplicate.
- We don't track changelogs or update history. Always maintain the current state.

**Filter out implementation details:**
- Skip anything about code structure, tech stack, build system, or internal architecture.
- Keep only facts that affect what a reader would see, search for, or care about.

## Handling bulk context

If the user shares a lot of context at once, break it into the right sections. Keep facts that affect SEO content. Skip internal details that do not matter to readers.

## Confirm

After writing, show a short summary:

```
Updated seo-memory.md:
- [Offerings > Keyword Explorer] Added benefit: "Find low-competition keywords without manual SERP checking"
- [Pricing] Updated free tier limit from 50 to 100 keywords
```

Do not dump the full file contents.
