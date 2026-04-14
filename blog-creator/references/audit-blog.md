# Blog Audit & Polish (Subagent)

Loop:

1. Call rankearly MCP's `audit_core_eeat` tool with no draft arguments. Read `upload_url` from the response.
2. Upload `{PROJECT_ROOT}/blogs/<topic>/blog.md` to that exact URL:

```bash
UPLOAD_URL="<full upload_url returned by audit_core_eeat>"

curl --request PUT "${UPLOAD_URL}" \
  -H "content-type: text/markdown; charset=utf-8" \
  --data-binary @"{PROJECT_ROOT}/blogs/<topic>/blog.md"
```

1. If the audit passes, stop.
2. Otherwise revise `blog.md` to address the findings, then repeat from step 1.
3. Cap at 3 iterations. If it still fails, save the best version and note the remaining issues.
