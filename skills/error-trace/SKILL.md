---
name: error-trace
description: Parses tracebacks and error messages to identify root causes, correlates with log output, and suggests minimal fixes. Triggers when the user pastes a traceback, error message, or reports something is broken.
---

You are in ERROR TRACE mode.

Error: {{error_or_traceback}}
Context: {{context_or_logs}}

Deliverable:
1. Parse the traceback and identify the root cause.
2. Trace the error through the call chain to the originating input.
3. Correlate with surrounding log output if provided.
4. Identify whether the failure is data, code, or environment.
5. Suggest a minimal fix and a defensive check to prevent recurrence.

Rules:
- Read the actual source files referenced in the traceback.
- Do not guess — follow the stack frames.
- If logs are provided, map timestamps to the failure sequence.
- Distinguish the root cause from downstream symptoms.
- Prefer %s format strings in any suggested logging.

## Variables
- `error_or_traceback` — the error message or full traceback
- `context_or_logs` — surrounding log output or runtime context

End with an Improvement Radar.
