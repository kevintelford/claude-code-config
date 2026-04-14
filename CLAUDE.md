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

## Secure coding (OWASP Top 10 + general)
Always write secure code by default. Don't wait for a security review to fix these:
- **Injection**: Parameterize all queries (SQL, NoSQL, OS commands, LDAP). Never build queries via string concatenation with user input. Use ORMs or parameterized APIs.
- **XSS**: Escape/sanitize all user-supplied content before rendering in HTML. Use framework-provided escaping (Jinja2 autoescape, React JSX).
- **Authentication/Authorization**: Don't roll custom auth. Use established libraries. Check permissions on every endpoint, not just the UI. Validate JWTs properly.
- **Secrets management**: Never hardcode API keys, passwords, or tokens. Use env vars or a secrets manager. Don't log secrets. Don't commit `.env` files.
- **Input validation**: Validate at system boundaries — user input, API parameters, file uploads, webhook payloads. Reject unexpected types/sizes/formats early.
- **Dependency security**: Keep dependencies updated. Audit for known CVEs (`uv audit`, `pip-audit`). Pin versions in production.
- **Path traversal**: Validate file paths. Don't allow user input to construct file paths without sanitization. Reject `../` patterns.
- **Error handling**: Don't expose stack traces, internal paths, or system details in user-facing errors. Log details server-side, return generic messages to clients.
- **CORS/CSRF**: Configure CORS restrictively. Use CSRF tokens for state-changing operations.

## LLM application security (OWASP Top 10 for LLMs)
When writing code that involves LLM calls, RAG pipelines, or user-facing AI features, keep these in mind:
- **Prompt injection**: Treat all document content and user input as untrusted. RAG chunks should never modify system prompt behavior. Validate/sanitize inputs before injecting into prompts.
- **Sensitive data in outputs**: LLM outputs may echo sensitive content from input documents. Don't log full outputs at INFO level. Sanitize client names in benchmark data, holdfast evidence, and any file that could be committed to git.
- **System prompt leakage**: Prompts contain proprietary methodology. Never expose system prompts via API responses, error messages, or debug output.
- **Vector/embedding poisoning**: Documents loaded into vector DBs are untrusted. Validate before ingestion. Monitor for anomalous retrieval results.
- **Unbounded consumption**: Cap concurrent LLM calls (max_workers), enforce retry limits, track token usage. A runaway loop can burn through API budget fast.
- **Output validation**: Always validate LLM structured output against the expected schema before using it downstream. Don't trust that the model returned what you asked for.

## Git commit policy
- **Default**: Make code changes freely, but do NOT commit unless explicitly asked.
- Per-project override: If a project's `CLAUDE.md` says "auto-commit allowed", then commit after completing work.
- When asked to commit, follow the standard commit protocol (status, diff, log, then commit).

## Scope toggle
If the user says **"include improvements"**, you may implement only 1–2 S-sized radar items.
