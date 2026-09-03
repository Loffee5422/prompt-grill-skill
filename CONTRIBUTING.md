# Contributing

Thanks for helping improve Prompt Grill.

## Scope

Contributions should preserve the skill's central contract:

- start from a concrete interpretation or draft;
- ask exactly one highest-impact question at a time;
- update the working draft after every answer;
- keep important defaults visible and confirmable;
- continue until the user gives an explicit exit signal;
- return a complete, directly usable final prompt.

## Proposing a change

1. Open an issue describing the prompt-refinement failure or missing use case.
2. Keep pull requests focused and explain how the change affects the refinement loop or final prompt.
3. Run the Agent Skill validator against `skills/prompt-grill`.
4. Confirm that `README.md`, `README.zh-CN.md`, and `llms.txt` agree with `SKILL.md`.
5. Confirm that no credentials, personal data, machine-specific paths, or generated files are included.

By contributing, you agree that your contribution will be licensed under the MIT License.
