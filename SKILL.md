---
name: delegate-grill-with-docs
description: Run grill-with-docs with the main agent asking questions and one inherited subagent answering as the user's proxy. Use when Codex should preserve the original multi-round grill-with-docs interview flow, but delegate the user's answers to a single subagent that can inspect code and docs.
---

# Delegate Grill With Docs

## Workflow

1. Spawn exactly one worker subagent.
2. Fork the current context into it.
3. Leave `model` and `reasoning_effort` unset so the subagent inherits the parent agent's model and reasoning strength.
4. The main agent runs the [grill-with-docs](https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs) workflow as the interviewer.
5. Tell the subagent to act as the user's proxy: answer the main agent's questions using the repository, existing docs, and current conversation context.
6. The main agent asks exactly one grill-with-docs question at a time.
7. Send each question to the same subagent, wait for its answer, then evaluate whether the answer is sufficient or another question is needed.
8. Repeat this main-agent-question/subagent-answer loop until the main agent has enough information to stop asking.
9. If the subagent cannot infer an answer from available evidence, it must say what is unknown and what only the real user can decide.
10. After the questioning is complete, the main agent combines the subagent's answers with the target document, updates `CONTEXT.md` or ADRs when required by the grill-with-docs workflow, and writes the agreed edits back to the original document.
11. Stop after one subagent. Do not fan out or replace it mid-session.

## Guardrails

- Trigger only when the user explicitly invokes `$delegate-grill-with-docs` or names this skill directly.
- Do not auto-run just because the user mentions `grill-with-docs`.
- Do not ask the real user to answer questions that the subagent can infer from the repo or existing context.
- Do not let the subagent choose the interview agenda; the main agent owns the grill-with-docs questioning loop and final document edits.
- Preserve the project's glossary. If a term conflicts with `CONTEXT.md`, flag it immediately.
- Update `CONTEXT.md` inline when a durable term is resolved. Create an ADR only for hard-to-reverse decisions.
- If the user explicitly wants the original live grilling flow, skip delegation and run it directly.
