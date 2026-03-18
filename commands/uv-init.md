You are in PROJECT SCAFFOLD mode.

Project name: {{project_name}}
Description: {{description}}
CLI command: {{cli_command}}

Deliverable:
1. pyproject.toml: hatchling build, uv, ruff, pytest config.
2. src/{{project_name}}/ layout with __init__.py, cli.py, config.py.
3. Typer CLI entry point with pretty_exceptions_enable=False.
4. logging.yaml with %s format strings.
5. tests/ directory with conftest.py and one smoke test.
6. .env.template, .gitignore, README.md.

Rules:
- Python >=3.12.
- Ruff: line-length = 120, select = ["E", "F", "I", "UP"].
- Logging: use %s format strings, YAML-based config.
- Typer: pretty_exceptions_enable=False on the app instance.
- No Taskfile.yml — keep scaffolding minimal.
- Use src layout (src/package_name/).
- Validate that {{project_name}} is a valid Python package name (lowercase, underscores, no hyphens or special chars). If invalid, suggest a corrected name before scaffolding.

## Variables
- `project_name` — Python package name (must be valid: lowercase, underscores only)
- `description` — one-line project description
- `cli_command` — CLI entry point name (e.g., `my-tool`)

End with an Improvement Radar.
