# Blog Audit & Polish (Subagent)

Loop:

1. Call rankearly MCP's `audit_content_quality` tool. Pass `url` for a published page, or omit `url` to audit a local draft file. Read the curl command from the response.
2. Run the returned curl command. The response body is the formatted audit report.

URL mode (published page) — run the curl exactly as returned, e.g.:

```bash
curl --max-time 120 --request PUT "<upload_url>"
```

Draft file mode — replace the placeholder path with the real file path:

```bash
UPLOAD_URL="<full upload_url returned by audit_content_quality>"

curl --max-time 120 --request PUT "${UPLOAD_URL}" \
  -H "content-type: text/markdown; charset=utf-8" \
  --data-binary @"{PROJECT_ROOT}/blogs/<topic>/blog.md"
```

3. If the audit passes, stop.
4. Otherwise revise `blog.md` to address the findings, then repeat from step 1.
5. Cap at 3 iterations. If it still fails, save the best version and note the remaining issues.
