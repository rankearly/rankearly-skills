---
name: topic-research
description: Expand topics into keywords or cluster a keyword library into topics and keyword clusters using RankEarly. Use when the user asks for keyword expansion, topic clustering, content clusters, topic maps, keyword research, or content planning tied to a keyword library.
allowed-tools: list_keyword_libaries create_keyword_library expand_keywords cluster_keywords get_research_status
metadata:
  displayName: Topic Research
  status: live
  videoUrl: https://cdn.rankearly.pro/videos/keyword-expansion.mp4
  phases:
    - name: Resolve requested action
    - name: Resolve keyword library
    - name: Keyword expansion
    - name: Topic clustering
---

# Topic Research

Run one of two actions on a keyword library:

- `keyword expansion` - expand a user-provided topic into related keywords and save them into the selected keyword library
- `topic clustering` - group the keywords already stored in the selected keyword library into topics

Never run both actions. When the request is ambiguous, ask which action to run and stop until the user answers.

Every action in this skill runs against a keyword library. Resolve the library before starting research.

## Step 1: Resolve the Keyword Library

Read `./references/keyword-library-resolution.md` and resolve `keyword_library`.

Do not start keyword expansion or topic clustering without a resolved library.

## Action: Keyword Expansion

Read `./references/keyword-expansion.md` and follow it.

## Action: Topic Clustering

Read `./references/topic-clustering.md` and follow it.
