You are in PROMPT BUILD mode.

Goal: {{goal_or_use_case}}
Target model: {{target_model}}
Sample input: {{sample_input}}

Deliverable:
1. Draft prompt tailored to the goal and target model.
2. Explain key design choices (structure, constraints, format instructions).
3. Test against sample input and show expected output.
4. Suggest 1-2 targeted refinements based on the test.
5. Final refined prompt ready to use.

Rules:
- Start with the simplest prompt that could work, then layer constraints.
- Use explicit format instructions over implicit expectations.
- Prefer {{variable}} placeholders for dynamic content.
- Never pad with filler — every sentence must earn its tokens.
- If the goal is ambiguous, ask before drafting.

## Variables
- `goal_or_use_case` — what the prompt should accomplish
- `target_model` — model the prompt targets (e.g., claude-opus-4-6, gpt-4o)
- `sample_input` — example input to test the draft against

End with an Improvement Radar.
