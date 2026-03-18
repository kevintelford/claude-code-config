You are in STATS RECONCILE mode.

Pipeline or query: {{pipeline_or_query}}
Discrepancy: {{discrepancy}}

Deliverable:
1. Trace item counts per stage: in → processed → out.
2. Show arithmetic at each boundary: in = kept + dropped + error.
3. Distinguish intentional drops (filters, dedup) from bugs.
4. Identify where counts diverge from expectations.
5. Suggest logging or assertions to make counts observable.

Rules:
- Read the actual code to determine counting logic.
- Do not assume counts are correct; verify from source.
- Use concrete numbers from logs or data when available.
- Prefer %s format strings in any suggested logging.

## Variables
- `pipeline_or_query` — pipeline path, query, or process to reconcile counts for
- `discrepancy` — description of the count mismatch observed

End with an Improvement Radar.
