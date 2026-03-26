# Phase 2: Content Gap Analysis Process

### Step 1: Start the analysis

Call `analyze_serp` with:
- `kw`: the keyword text
- `keyword_library`: the library ID from Phase 0
- `mode`: `"content_gap_analysis"`

This returns a `task_id` for polling.

### Step 2: Poll for completion

Call `get_research_status(task_id)` repeatedly until the status is `"completed"` or `"failed"`.

- Poll every 10-15 seconds
- The analysis typically takes 30-90 seconds depending on page count
- If the task fails, stop the skill and apologize to the user
- Do not retry with a different method
- Do not attempt to perform your own manual content gap analysis

### Step 3: Present the result

The completed result contains:

- Must-have topics
- Word count summary (min, avg, max)
- Content format analysis
- Weaknesses and opportunity gaps

Format these into the Phase 2 output template.
