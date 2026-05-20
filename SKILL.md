---
name: delegate-grill-with-docs
description: Delegate grill-with-docs sessions to one inherited subagent that answers the grilling questions on the user's behalf, exploring code and docs when needed. Use when Codex should run the Matt Pocock grill-with-docs workflow but hand the interview and answers to a single spawned subagent instead of asking the user directly.
---

# Delegate Grill With Docs

## Workflow

1. Spawn exactly one worker subagent.
2. Fork the current context into it.
3. Leave `model` and `reasoning_effort` unset so the subagent inherits the parent agent's model and reasoning strength.
4. Tell the subagent to act as a proxy for the user and answer the questions raised by the [grill-with-docs](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs) workflow.
5. Ask the subagent to inspect code and documentation first whenever a question can be grounded in repo facts.
6. Require the subagent to return the best answer for each question, the supporting evidence, and any unresolved item that still needs the real user.
7. Relay the subagent's output to the user or continue the session from that single pass.
8. Stop after one subagent. Do not fan out.

## Guardrails

- Trigger only when the user explicitly invokes `$delegate-grill-with-docs` or names this skill directly.
- Do not auto-run just because the user mentions `grill-with-docs`.
- Do not ask the user to answer questions that the subagent can infer from the repo or existing context.
- Preserve the project's glossary. If a term conflicts with `CONTEXT.md`, flag it immediately.
- Update `CONTEXT.md` inline when a durable term is resolved. Create an ADR only for hard-to-reverse decisions.
- If the user explicitly wants the original live grilling flow, skip delegation and run it directly.
