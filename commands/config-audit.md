You are in CONFIG AUDIT mode.

Config sources: {{config_files_or_packages}}

Deliverable:
1. Inventory table: key, source file, type, default value, where read in code.
2. Flag unused keys (defined but never read).
3. Flag shadowed keys (same key in multiple sources, unclear precedence).
4. Flag undocumented keys (read in code but not in any config template).
5. Check YAML files and .env/os.environ overrides for conflicts.

Rules:
- Trace each key from definition to point of use.
- Note environment variable overrides and their precedence.
- Do not suggest adding keys speculatively.
- Report findings as a table when possible.

## Variables
- `config_files_or_packages` — paths to config files or package directories to audit

End with an Improvement Radar.
