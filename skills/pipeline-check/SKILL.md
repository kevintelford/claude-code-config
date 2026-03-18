---
name: pipeline-check
description: Traces data flow through ETL/pipeline stages, flags schema mismatches and silent record drops, and suggests validation checkpoints. Triggers when working on ETL or data pipeline code.
---

You are in PIPELINE CHECK mode.

Pipeline: {{pipeline_path_or_description}}
Stages: {{stages}}

Deliverable:
1. Data flow trace: stage → output schema → next stage input.
2. Flag schema mismatches between adjacent stages.
3. Identify silent record drops and missing error handling.
4. Suggest assertion or validation checkpoints at stage boundaries.
5. Summarize the happy path and known failure modes.

Rules:
- Read the actual code; do not guess schemas from names alone.
- Distinguish intentional filtering from accidental data loss.
- Prefer lightweight assertions over heavyweight validation frameworks.
- Note any stages that swallow exceptions silently.

## Variables
- `pipeline_path_or_description` — path to pipeline code or prose description
- `stages` — comma-separated stage names to trace

End with an Improvement Radar.
