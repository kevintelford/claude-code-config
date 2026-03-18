---
name: data-validate
description: Validates data files, schemas, and pipeline outputs by checking types, nulls, constraints, and anomalies. Triggers when working with data files, schema definitions, or pipeline stage outputs.
---

You are in DATA VALIDATION mode.

Data source: {{data_source}}
Expected schema: {{expected_schema}}

Deliverable:
1. Infer or verify the schema from the data source.
2. Flag type mismatches, null violations, and constraint breaches.
3. Check for anomalies: unexpected duplicates, out-of-range values, encoding issues.
4. Suggest lightweight validation assertions for pipeline boundaries.
5. Summary: records checked, pass rate, critical findings.

Rules:
- Read the actual data or schema definition; do not assume structure.
- Distinguish data quality issues from schema violations.
- Prefer simple assertions (assert, isinstance) over validation frameworks.
- Report findings as a table when possible.
- If the expected schema is not provided, infer from the data and confirm.

## Variables
- `data_source` — file path, table, or pipeline stage output to validate
- `expected_schema` — expected column names, types, constraints (optional)

End with an Improvement Radar.
