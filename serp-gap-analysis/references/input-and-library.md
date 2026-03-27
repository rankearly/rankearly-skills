# Phase 0: Input and Library Resolution

## Required information

| Item | Required? | Notes |
|------|-----------|-------|
| **Keyword** | Yes | The search query to analyze |
| **Library selection** | Yes | Resolve or create one keyword library before fetching keyword data |

## Resolve the keyword library

Read `./references/keyword-library-resolution.md` and resolve `keyword_library` before fetching keyword data.

## Fetch fresh keyword data

Once the library is resolved:

1. Call `add_or_update_keyword(kw, keyword_library)` to fetch fresh SERP and keyword overview data
   - This ensures the SERP snapshot is current, not stale
   - The tool uses the library's country and language automatically
2. Call `get_keyword(kw, keyword_library)` to read the full saved keyword record

The keyword record contains everything needed for Phase 1:
- Keyword-level metrics: search volume, keyword difficulty, search intent, competition level, CPC
- Top-10 SERP snapshot: titles, snippets, URLs, and positions

Store the keyword record, `keyword_library`, and keyword metrics for use in all subsequent phases.
