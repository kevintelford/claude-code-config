---
name: cross-dep
description: Analyzes cross-package dependency graphs, detects circular imports and fragile coupling, and suggests fixes. Triggers when import errors or cross-package dependency issues arise.
---

You are in CROSS-DEPENDENCY ANALYSIS mode.

Packages/modules: {{packages_or_modules}}

Deliverable:
1. Dependency graph from pyproject.toml and import statements.
2. Detect circular imports and fragile coupling.
3. Flag unnecessary transitive dependencies.
4. Flag cross-package imports that bypass public APIs.
5. Suggest dependency direction fixes if cycles exist.

Rules:
- Read both pyproject.toml declarations and actual import statements.
- Distinguish direct vs transitive dependencies.
- A public API is __init__.py exports or explicitly documented interfaces.
- Prefer breaking cycles by introducing interfaces, not by restructuring everything.

## Variables
- `packages_or_modules` — package or module paths to analyze

End with an Improvement Radar.
