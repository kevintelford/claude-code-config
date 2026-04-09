# Personal Claude Preferences

## Communication style
- Be direct and honest. If an idea is good, say so. If it's not great, say that too with a clear reason.
- No sugarcoating, no hedging, no "that's a great question" filler.
- Skip the diplomatic sandwich — just give the straight take.

## Logging style
- Use %s for all logging format strings, not %d or %f
- Example: `logger.info("Processing %s items", count)`

## Primary goals
1. Write minimal, readable Python.
2. Iterate safely with small diffs.
3. Plan before implementing medium or large features.
4. Surface improvement opportunities without scope creep.

## Python style preferences
- Prefer functions over classes unless state is required.
- Use `dataclasses` for simple structured data.
- Prefer explicit types (`typing`) where helpful, but avoid noise.
- Avoid metaprogramming, decorators, and magic unless clearly beneficial.
- Prefer clarity over Python cleverness.

## Python project defaults
- Python >=3.12
- Build backend: hatchling
- Project structure: src layout (`src/package_name/`)
- Ruff: line-length = 120, select = ["E", "F", "I", "UP"]
- Logging: YAML-based config, %s format strings
- Dependency management: uv

## CLI preferences
- For Typer apps: disable rich exception formatting (`pretty_exceptions_enable=False`)
- Use plain Python tracebacks, not fancy boxes

## Spec location
Save design specs to `.claude/plans/` in the project directory (not `docs/superpowers/specs/`).

## Plan threshold
Plan first if any are true:
- touches more than one module
- changes public interfaces
- introduces new dependencies
- modifies persistence, I/O, or concurrency
- likely diff > ~30 lines

Plans are written to `.claude/plans/` in the project directory (the default location). After finishing a plan, always tell the user the exact file path (e.g., `.claude/plans/some-name.md`) so they can find it later.

## Diff discipline
- Change only what is required.
- No formatting-only diffs.
- No opportunistic refactors.
- Suggest improvements separately.
- After modifying files, always provide a summary of what changed and which files were touched.
- After making code changes, review and update any relevant README or documentation files to keep them in sync (new CLI flags, config options, changed behavior, etc.).

## Backwards compatibility
Do NOT add backwards compatibility code by default. This includes:
- Renaming variables to `_unused_var` instead of deleting
- Re-exporting removed types/functions
- Adding `# removed` comments for deleted code
- Shims or adapters for old interfaces

If something is unused, delete it completely.

**Exception**: Say "include backwards compat" to preserve compatibility for a specific change.

## Improvement Radar (coding tasks only)
Only include the radar when the response involves writing or modifying code (features, bug fixes, refactors, tests). **Skip the radar** for data processing, config changes, documentation, plan discussions, and non-coding tasks.

When included:

### Improvement Radar
- Max 5 items, numbered (1-5)
- Format: N. [Category] What — why it matters (Effort: S/M/L)
- Categories: correctness, clarity, tests, performance, security, observability

Never include radar items directly in the diff unless explicitly requested.

## Auto-trigger skills
Invoke these skills automatically when the trigger condition is met:

- `/plan` — Task hits the plan threshold (see above). Do not implement until the plan is approved.
- `/tests` — After implementing a non-trivial change, propose test cases before moving on.

Do not auto-trigger when the user is clearly asking for something simpler (e.g., a one-line fix doesn't need `/plan`). When in doubt, just do the work — don't force a skill invocation.

## Sensitive content guardrail
Files in this repo (`dotfiles/claude/`) are shared and version-controlled. Before writing or editing any file here, check for:
- Client or project names
- Company-specific variable names, paths, or URLs
- API keys, tokens, or credentials
- Internal tool names or infrastructure details
- Any content that identifies a specific engagement or employer

If anything looks project-specific or potentially sensitive, **stop and ask** before writing it. Prefer generic placeholders (`{{variable}}`) over concrete values.

## Scope toggle
If the user says **"include improvements"**, you may implement only 1–2 S-sized radar items.
