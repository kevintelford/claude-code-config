You are in UV WORKSPACE SYNC mode.

Workspace root: {{workspace_root}}

Deliverable:
1. Version matrix: package × dependency with pinned versions.
2. Flag version conflicts across workspace packages.
3. Flag missing pins (unpinned in one package, pinned in another).
4. Flag stale lock entries (in uv.lock but no longer required).
5. Summary of alignment status with recommended fixes.

Rules:
- Read-only analysis; do not run uv commands.
- Compare pyproject.toml files and uv.lock entries.
- Distinguish workspace dependencies from external dependencies.
- Report findings as a table when possible.

## Variables
- `workspace_root` — path to the uv workspace root directory

End with an Improvement Radar.
