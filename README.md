# Prompt Grill: refine vague ideas into ready-to-use prompts

Prompt Grill is an Agent Skill for turning an unclear prompt idea into a user-approved prompt that can be used immediately. Its defining behavior is a visible, iterative refinement loop: form a concrete interpretation first, ask exactly one high-impact question, update the draft, and continue until the user explicitly says to finish.

[简体中文](README.zh-CN.md)

## Install

Canonical skill URL:

```text
https://github.com/Loffee5422/prompt-grill-skill/tree/main/skills/prompt-grill
```

Paste this instruction into a compatible agent:

```text
Install the `prompt-grill` skill from https://github.com/Loffee5422/prompt-grill-skill/tree/main/skills/prompt-grill
```

With Codex's bundled GitHub skill installer:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --url https://github.com/Loffee5422/prompt-grill-skill/tree/main/skills/prompt-grill
```

For reproducible installation, pin the initial release:

```text
https://github.com/Loffee5422/prompt-grill-skill/tree/v1.0.0/skills/prompt-grill
```

## What it does

- Starts from the user's existing idea, even when it is rough.
- Brings a concrete interpretation or draft to each clarification instead of asking empty-context questions.
- Asks only one question at a time, choosing the ambiguity with the greatest effect on output quality.
- Updates the working prompt after every answer and briefly explains what changed.
- Challenges vague answers with a reasonable default while keeping important decisions visible to the user.
- Continues refining until the user gives an explicit stop or finish signal.
- Produces one complete, directly usable prompt at the end.

## Representative uses

- Turn a rough idea into a system prompt for Claude, ChatGPT, Codex, or another model.
- Refine a reusable prompt for a product feature or internal workflow.
- Clarify output format, tone, constraints, edge cases, examples, and success criteria.
- Improve an existing prompt whose results are inconsistent or underspecified.

## Requirements and compatibility

Prompt Grill is written for agents that support the Agent Skills `SKILL.md` format. It has no scripts, external services, or runtime dependencies. The conversation can happen in any language the agent and user share; the operational instructions are in Simplified Chinese.

The skill creates prompt text only. It does not automatically run the finished prompt in another system or modify external applications.

## How it works

The agent maintains a working draft and repeatedly selects the single unresolved issue most likely to affect the result. It prioritizes the target user and execution context, desired output, constraints, edge cases, examples, and success criteria. After every response, it updates the draft and keeps the user aware of the evolving interpretation.

The loop ends only when the user signals that the prompt is satisfactory or asks to stop questioning. The agent then returns a clean final prompt without unrelated commentary inside it.

The complete operating instructions live in [`skills/prompt-grill/SKILL.md`](skills/prompt-grill/SKILL.md).

## Example

User:

> I need a prompt that reviews my writing.

Prompt Grill first states a concrete interpretation—for example, that the prompt is meant for repeated use with a general-purpose model—then asks the one most consequential unresolved question. After each answer, it shows what changed and asks only the next highest-value question.

## FAQ

### Does it ask a fixed checklist of questions?

No. The question count and order follow the ambiguity in the current draft. A simple request may need only a few rounds; a complex prompt may need more.

### Why only one question at a time?

The design keeps each decision easy to answer and makes it clear which new information changed the draft.

### When does the interview stop?

It stops when the user gives a clear exit signal such as “that works,” “stop,” or “just give me the final prompt.” It should not finish early merely because several questions have already been answered.

### What if the user says “you decide”?

The agent proposes a sensible default and briefly explains it, but asks the user to confirm or change important decisions.

### Does every final prompt use a rigid template?

No. The final prompt includes the necessary context, goal, input and output requirements, constraints, edge-case behavior, or examples naturally, without forcing unnecessary headings.

## Limitations

- The final prompt reflects the information and decisions surfaced during the conversation.
- The skill improves specification and alignment; it does not guarantee the behavior of every downstream model or tool.
- It is intentionally interactive and is not designed for one-shot prompt generation when the user does not want clarification.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Contributions should preserve the one-question-at-a-time loop, visible draft evolution, and explicit user-controlled exit.

## License

Released under the [MIT License](LICENSE).
