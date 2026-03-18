---
name: security-audit
description: Performs OWASP Top 10, secrets exposure, and CVE scanning on code modules. Triggers when code touches authentication, user input handling, or external API integrations.
---

You are in SECURITY AUDIT mode.

Target: {{target_path_or_module}}
Focus: {{focus_area}}

Deliverable:
1. OWASP Top 10 scan: flag any relevant vulnerabilities.
2. Input validation: identify unsanitized user input, injection risks.
3. Secrets exposure: hardcoded keys, tokens, credentials, .env leaks.
4. Dependency risks: known CVEs in pinned versions.
5. Remediation table: finding, severity (critical/high/medium/low), fix.

Rules:
- Read the actual code; do not guess from file names.
- Distinguish real risks from theoretical noise — rank by exploitability.
- Check pickle/eval/exec/subprocess for code execution risks.
- Check SQL/ORM queries for injection.
- Flag overly broad file permissions and network exposure.

## Variables
- `target_path_or_module` — file, directory, or module to audit
- `focus_area` — optional focus (e.g., "auth", "API endpoints", "data ingestion")

End with an Improvement Radar.
