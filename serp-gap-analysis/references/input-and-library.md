# Phase 0: Input and Library Resolution

## Required information

| Item | Required? | Notes |
|------|-----------|-------|
| **Keyword** | Yes | The search query to analyze |
| **Library selection** | Yes | The user must pick one option from the library list |

Start with an `AskUserQuestion` that lets the user select one library option.

## Resolve the keyword library

1. Call `list_keyword_libaries`.
2. Use `AskUserQuestion` to present the available libraries as selectable options, plus one final option for creating a new library.
3. Format the options like this:

   ```text
   1. library1 - United States, English
   2. library2 - United Kingdom, English
   3. New library - specify the country and language
   ```

4. If the user selects an existing library, continue with that library ID.
5. If the user selects `New library`, collect country and language with `AskUserQuestion` when they are not already provided.
6. Call `create_keyword_library` with the chosen country and language for the new library.
   - Recommended naming format: `Keywords_{COUNTRY}_{LANGUAGE}`, e.g. `Keywords_US_EN`
7. Continue with the selected or newly created library ID.

## Fetch fresh keyword data

Once the library is resolved:

1. Call `add_or_update_keyword(kw, keyword_library)` to fetch fresh SERP and keyword overview data
   - This ensures the SERP snapshot is current, not stale
   - The tool uses the library's country and language automatically
2. Call `get_keyword(kw, keyword_library)` to read the full saved keyword record

The keyword record contains everything needed for Phase 1:
- Keyword-level metrics: search volume, keyword difficulty, search intent, competition level, CPC
- Top-10 SERP snapshot: titles, snippets, URLs, and positions

Store the keyword record, library ID, and keyword metrics for use in all subsequent phases.
