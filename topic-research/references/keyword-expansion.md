# Keyword Expansion

Run keyword expansion against the resolved `keyword_library`.

## Gather Input

Infer the input mode from the user's request:

- **Topic** — when the user describes a topic, product, feature, or content idea
- **Keywords** — when the user provides a comma-separated list of seed keywords

If the user provides neither a topic nor seed keywords, ask them to provide one. Never hallucinate input.

**Topic mode**: The user may provide:
- a document or local file path
- a URL
- a brief product or topic description
- code files
- community discussions, user feedback, customer questions

Read the provided content and convert it into a markdown topic. Requirements: at least 20 characters, less than 400 words, user-centric and honest.

**Keywords mode**: Parse the user's comma-separated keywords (1-30 keywords).

## Infer Effort Level

Effort controls how many seeds are used:

| Effort | Value | Max Seeds |
|--------|-------|-----------|
| Ultra Low | `xlow` | 1 |
| Low | `low` | 5 |
| Medium | `medium` | 10 |
| High | `high` | 20 |
| Ultra High | `xhigh` | 30 |

Infer effort from the topic breadth or seed count:

| Effort | When to Use |
|--------|-------------|
| `xlow` | A specific keyword to expand |
| `low` | Niche topic or explicit low-effort request |
| `medium` | Common, specific topic (default) |
| `high` | Broad topic with diverse angles |
| `xhigh` | Explicit request for extensive search |

For keywords mode: if seed count exceeds the inferred effort's limit, use a higher effort.

## Run Expansion

1. Call `expand_keywords` with the appropriate parameters:
   - Topic mode: `expand_keywords(topic, keyword_library, effort)`
   - Keywords mode: `expand_keywords(seeds, keyword_library, effort)`
2. Poll `get_research_status(task_id)` until `"completed"` or `"failed"`. Wait 30 seconds before the first poll, then wait 10 seconds between each subsequent poll.
3. Report results when complete.

Expansion runs exactly once per call — no retry loop. If the user wants more keywords, run another expansion with a different topic or higher effort.

Stop after keyword expansion unless the user also explicitly requested topic clustering.
