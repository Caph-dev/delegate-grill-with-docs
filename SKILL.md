---
name: delegate-grill-with-docs
description: Run grill-with-docs through one inherited subagent while preserving the original multi-round interview flow. Use when Codex should keep one delegated interviewer in the loop and relay user answers back and forth until the discussion is complete.
---

# Delegate Grill With Docs

## Workflow

1. Spawn exactly one worker subagent.
2. Fork the current context into it.
3. Leave `model` and `reasoning_effort` unset so the subagent inherits the parent agent's model and reasoning strength.
4. Tell the subagent to act as the interview lead for the [grill-with-docs](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs) workflow and keep the conversation open until it has enough information to finish.
5. Require the subagent to ask exactly one question at a time, wait for the answer, then decide whether another question is needed.
6. Ask the subagent to inspect code and documentation first whenever a question can be grounded in repo facts.
7. Relay each subagent question to the user, capture the user's answer, and send that answer back to the same subagent.
8. Repeat the relay loop until the subagent explicitly says the discussion is complete or no more questions are needed.
9. When the subagent finishes, relay its final recommendation, supporting evidence, and any unresolved items, then apply the agreed document edits.
10. Stop after one subagent. Do not fan out or replace it mid-session.

## Guardrails

- Trigger only when the user explicitly invokes `$delegate-grill-with-docs` or names this skill directly.
- Do not auto-run just because the user mentions `grill-with-docs`.
- Do not ask the user to answer questions that the subagent can infer from the repo or existing context.
- Preserve the project's glossary. If a term conflicts with `CONTEXT.md`, flag it immediately.
- Update `CONTEXT.md` inline when a durable term is resolved. Create an ADR only for hard-to-reverse decisions.
- If the user explicitly wants the original live grilling flow, skip delegation and run it directly.
