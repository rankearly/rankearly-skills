# Keyword Expansion

Run keyword expansion against the resolved `keyword_library`.

## Gather or Confirm Topics

Ask the user to explicitly specify what topic or topics to gather before collecting context. For example:

- a document or local file path
- a URL
- a brief product or topic description
- code files
- ...

Any format is acceptable as long as it gives enough context to define a valid topic for SEO planning.

For the gathered context, turn it into a markdown topic that the user wants to use for keyword expansion.

Topic content requirements:
- less than 400 words
- user-centric and honest
- describes what the product, feature, or service can actually support
- describes the realistic value it can bring to the audience

Pass the topic content directly to `expand_keywords`. Do not summarize the MCP internals to the user.

## Run Expansion

For each confirmed topic:

1. Call `expand_keywords(topic, keyword_library)` with the topic content.
2. Poll `get_research_status(task_id)` until `"completed"` or `"failed"`. Wait 30 seconds before the first poll, then wait 10 seconds between each subsequent poll.
3. If insufficient keywords are returned, retry with a refined topic description, up to 5 retries.
4. Report progress after each topic completes.

Target counts per topic:
- Narrow topic: 100-200 keywords (1-2 iterations)
- Broad topic: 300-500 keywords (3-5 iterations)

Stop after keyword expansion unless the user also explicitly requested topic clustering.
