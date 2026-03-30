# Topic Clustering

Cluster the existing keywords in the resolved `keyword_library`.

Do not run keyword expansion first unless the user explicitly requested both actions.

1. Call `cluster_keywords(keyword_library)` to start clustering.
2. Poll `get_research_status(task_id)` until completed or failed. Wait 30 seconds before the first poll, then wait 10 seconds between each subsequent poll.
3. Review the resulting pillars and subtopics.
4. If the library does not contain enough keywords to cluster, stop and tell the user clustering needs keywords already present in that library.
