# Claude Code Custom Skills

Slash commands via `~/.claude/commands/` and auto-discovered skills via `~/.claude/skills/` (both symlinked from `dotfiles/claude/`).

## Directory Structure

```
dotfiles/claude/
├── commands/          # User-invoked slash commands (16)
├── skills/            # Auto-discovered skills (6)
│   ├── security-audit/SKILL.md
│   ├── error-trace/SKILL.md
│   ├── data-validate/SKILL.md
│   ├── dep-audit/SKILL.md
│   ├── pipeline-check/SKILL.md
│   └── cross-dep/SKILL.md
├── CLAUDE.md
└── README.md
```

## Commands (user-invoked)

| Command | Mode | Variables |
|---|---|---|
| `/prompt-review` | Prompt quality review | `prompt_files_or_text`, `target_model` |
| `/config-audit` | YAML/env config mapping | `config_files_or_packages` |
| `/stats-reconcile` | Pipeline count reconciliation | `pipeline_or_query`, `discrepancy` |
| `/uv-sync` | UV workspace dependency alignment | `workspace_root` |
| `/cover-letter` | Job application materials | `job_description`, `resume_or_background`, `company_name`, `tone` |
| `/uv-init` | Project scaffolding | `project_name`, `description`, `cli_command` |
| `/prompt-build` | Draft and refine prompts | `goal_or_use_case`, `target_model`, `sample_input` |
| `/plan` | Plan-first development | `task` |
| `/review` | Code review | `diff_or_pr` |
| `/fix` | Fix & diagnose | *(see file)* |
| `/implement` | Implement mode | *(see file)* |
| `/improve` | Improve mode | *(see file)* |
| `/iterate` | Iterate mode | *(see file)* |
| `/refactor` | Refactor proposal | *(see file)* |
| `/tests` | Tests mode | *(see file)* |
| `/doc` | Docs mode | *(see file)* |

## Skills (auto-discovered)

These trigger automatically based on context — no slash command needed.

| Skill | Mode | Trigger |
|---|---|---|
| `security-audit` | OWASP / secrets / CVE scan | Code touches auth, user input, or external APIs |
| `error-trace` | Traceback analysis and log correlation | User pastes a traceback or error message |
| `data-validate` | Schema and data quality checks | Working with data files, schemas, or pipeline outputs |
| `dep-audit` | CVEs, licenses, stale dependencies | Reviewing dependencies or updating packages |
| `pipeline-check` | ETL pipeline data flow trace | Working on ETL/pipeline code |
| `cross-dep` | Monorepo dependency analysis | Import errors or cross-package issues |

## Convention

### Commands
- Plain markdown, no frontmatter
- Mode declaration on line 1
- `{{variable}}` template syntax for user inputs
- Numbered **Deliverable** section
- **Rules** section (bulleted)
- **Variables** section documenting each template var
- Ends with "End with an Improvement Radar."

### Skills
- YAML frontmatter with `name` and `description` (under 1024 chars)
- Description includes what it does AND when to trigger
- Body content follows same convention as commands
- Lives in `skills/<skill-name>/SKILL.md`

## Adding a New Command

1. Create `command-name.md` in `commands/`
2. Follow the command convention above
3. The symlink makes it immediately available as `/command-name`

## Adding a New Skill

1. Create `skills/<skill-name>/SKILL.md`
2. Add YAML frontmatter with `name` and `description`
3. Follow the skill convention above
4. Claude auto-discovers it based on the description's trigger conditions
