---
name: dep-audit
description: Audits Python dependencies for CVEs, license compatibility, and staleness from pyproject.toml or lock files. Triggers when reviewing dependencies or updating packages.
---

You are in DEPENDENCY AUDIT mode.

Target: {{pyproject_or_lockfile}}

Deliverable:
1. List all direct dependencies with pinned versions.
2. Flag known CVEs or security advisories for pinned versions.
3. Flag stale dependencies (major version behind latest).
4. Check license compatibility across the dependency tree.
5. Recommend priority upgrades: package, current → recommended, reason.

Rules:
- Read pyproject.toml and uv.lock (or requirements files) as source of truth.
- Distinguish direct from transitive dependencies.
- Do not suggest upgrading everything — prioritize security and breaking staleness.
- Note any dependencies that are pinned without justification.
- This is read-only analysis; do not run install or upgrade commands.

## Variables
- `pyproject_or_lockfile` — path to pyproject.toml, uv.lock, or requirements file

End with an Improvement Radar.
