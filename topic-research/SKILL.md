---
name: topic-research
description: Build a pillar-cluster content architecture from a project's features, product characteristics, or service offerings using RankEarly's keyword expansion and clustering tools. Use when the user wants to do keyword research, find content topics, build a content strategy, create a topic map, or plan what articles to write for their site.
allowed-tools: expand_keywords cluster_keywords get_research_status fetch_data
metadata:
  displayName: Topic Research
  status: live
  phases:
    - name: Scan codebase for seed topics
    - name: Expand topics into keyword lists
    - name: Group into pillars and subtopics
---

# Topic Research

Build a pillar-cluster content architecture from a project's features, product characteristics, or service offerings.

Phases run sequentially. Each phase that uses a subagent runs one at a time (not in parallel) to avoid rate limit hits.

## Phase 0: Resolve Project and Keyword Library

Before delegating to subagents, resolve which project and keyword library to use.

Call `fetch_data` with the prompt `"fetch all projects and their keyword libraries"`.

| Projects | Libraries | Action |
|----------|-----------|--------|
| 0 | - | Tell the user: "You don't have any projects yet. Please create one in RankEarly first." Stop. |
| 1 | 0 | Tell the user: "Project **{name}** has no keyword libraries yet. Please create one in RankEarly first." Stop. |
| 1 | 1 | Use the single project and single library automatically. |
| 1 | 2+ | List the libraries and ask the user to pick one. |
| 2+ | - | List all projects with their libraries and ask the user to pick. |

Store `project_id` and `library_id` for all subsequent phases.

## Phase 1: Project Context Analysis (Subagent)

This phase involves heavy context — delegate to a **subagent** to keep the main context clean.

**Subagent instructions:**

1. Gather project context:
   - If the working directory has website code (Next.js, Vue, etc.), search locally for pages, features, components, copy, and marketing content
   - Otherwise, ask the user for a local website folder or a website URL or product description
2. Extract 5-15 seed topics from the gathered context
3. For each topic, write a description (min 20 characters, ideally 2-3 sentences describing the topic's relevance to the product)
4. Save output to `./topic-research/topics.md`

Expected file format:

```markdown
# Topics for {Project Name}

## 1. {Topic Title}
{2-3 sentence description of the topic and its relevance to the product}

## 2. {Topic Title}
{description}

...
```

**After the subagent completes:** Read `./topic-research/topics.md`, present the topics to the user, and **ask them to confirm or adjust** before proceeding to Phase 2.

## Phase 2: Keyword Expansion (Sequential)

For each confirmed topic, expand keywords **one topic at a time**.

**Tool specification:**
- `expand_keywords(project_id, library_id, content)` — starts async keyword expansion
  - `content`: Topic description (min 20 characters)
  - Returns: `research_id`

**Per-topic workflow:**
1. Call `expand_keywords(project_id, library_id, content)` with the topic description
2. Poll `get_research_status(research_id)` until `"completed"` or `"failed"`
3. If insufficient keywords (<100), retry with a refined description (max 5 retries)
4. Report progress to the user after each topic completes

Target keyword counts per topic:
- Narrow topic: 100-200 keywords (1-2 iterations)
- Broad topic: 300-500 keywords (3-5 iterations)

## Phase 3: Topic Clustering

Once all keywords are expanded:

1. Call `cluster_keywords(project_id, library_id)` to start clustering
2. Poll `get_research_status(research_id)` until completed
3. Review the resulting pillars and subtopics

## Output

The final output is a content architecture with:
- **10 content pillars** — broad topical themes
- **5-30 subtopics per pillar** — specific article ideas
- **Keyword clusters** — all related keywords per subtopic

Present a summary to the user and suggest next steps.
