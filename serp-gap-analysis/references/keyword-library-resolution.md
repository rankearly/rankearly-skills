# Keyword Library Resolution

1. Call `list_keyword_libaries`.
2. If the user already provided a library name or ID and exactly one library clearly matches it, use that library as `keyword_library`.
3. If the user explicitly asks to create a new keyword library, skip library selection and collect country and language.
4. If there are no libraries yet:
   - Ask whether to create a new keyword library.
   - If the user declines, stop.
   - Collect country and language.
5. Otherwise, when no library has been resolved yet, use `AskUserQuestion` to present the available libraries as selectable options, plus one final option:

   ```text
   1. Project A / library1 - United States, English
   2. Project B / library2 - United Kingdom, English
   3. New keyword library - specify the country and language
   ```

   Include the project name before each existing library option to avoid ambiguity when the user has multiple projects.

6. If the user selects an existing library, use that library as `keyword_library`.
7. If the user selects `New keyword library`, collect country and language when they are not already provided.
8. When creating a library, call `create_keyword_library` with a generated name using the recommended format `Keywords_{COUNTRY}_{LANGUAGE}`.
9. Store the selected or newly created library as `keyword_library`.

`create_keyword_library` creates the library in the user's most recently updated active project. Do not claim that the user can choose a different project through this tool.
