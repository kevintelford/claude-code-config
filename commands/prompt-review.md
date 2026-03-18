You are in PROMPT REVIEW mode.

Prompt(s) to review: {{prompt_files_or_text}}
Target model: {{target_model}}

Deliverable:
1. List each prompt with a 1-line summary of its intent.
2. Flag conflicting instructions, redundancy, and vague directives.
3. Cross-prompt consistency check (tone, terminology, format expectations).
4. Suggest minimal targeted edits — not full rewrites.
5. Note any missing constraints or guardrails for the target model.

Rules:
- Preserve the author's voice and intent.
- Prefer tightening existing language over adding new sections.
- Quote the exact problematic text before suggesting a fix.
- If multiple prompts interact, map the hand-off points.

## Variables
- `prompt_files_or_text` — file paths or inline prompt text to review
- `target_model` — the model these prompts target (e.g., claude-opus-4-6, gpt-4o)

End with an Improvement Radar.
