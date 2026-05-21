# delegate-grill-with-docs

`delegate-grill-with-docs` is a Codex skill for running a `grill-with-docs`-style discussion through one delegated subagent. When you explicitly invoke `$delegate-grill-with-docs`, Codex spawns one inherited subagent, relays questions and answers back and forth, and writes the final outcome back to the original document.

## Trigger

This skill only activates when you explicitly mention `$delegate-grill-with-docs`.

## Installation

### Fastest path for any agent

Send this repository link to your agent and ask it to install the workflow:

`https://github.com/Caph-dev/delegate-grill-with-docs`

Tell it to keep the repository available in the workspace, read `SKILL.md`, and wire the workflow into its own project-instruction system.

You can also paste this prompt directly into your agent:

```text
Install the skill from https://github.com/Caph-dev/delegate-grill-with-docs.
```

### Codex

Clone or copy the repository into your Codex skills directory:

```text
~/.codex/skills/delegate-grill-with-docs
```

Example:

```zsh
git clone https://github.com/Caph-dev/delegate-grill-with-docs ~/.codex/skills/delegate-grill-with-docs
```

After installing, restart Codex to pick up the new skill.

## Example Prompts

```text
For @xxx-doc.md, use $delegate-grill-with-docs for a deep discussion and write the final conclusions and required edits back into the original document.
```

```text
Use $delegate-grill-with-docs to grill the ideas in @xxx-doc.md, then apply the agreed changes directly back to the same document with minimal edits.
```

## Notes

- Use this skill only when you want Codex to delegate the discussion to one subagent and keep a multi-round interview going through that same agent.
- It does not auto-trigger just because `grill-with-docs` is mentioned.

---

## 中文说明

这个 skill 只在你显式写出 `$delegate-grill-with-docs` 时触发。即使提到 `grill-with-docs`，也不会自动触发这个 skill。

## 安装方式

### 最快方式（适用于所有 Agent）

把这个仓库链接发给你的 agent，让它替你安装这个 skill：

`https://github.com/Caph-dev/delegate-grill-with-docs`

告诉它把仓库保留在工作区里，读取 `SKILL.md`，并接到它自己的项目指令系统中。

你也可以直接把下面这段发给你的 agent：

```text
安装来自 https://github.com/Caph-dev/delegate-grill-with-docs 的 skill。
```

### Codex

将仓库克隆或复制到 Codex 的 skills 目录：

```text
~/.codex/skills/delegate-grill-with-docs
```

示例：

```zsh
git clone https://github.com/Caph-dev/delegate-grill-with-docs ~/.codex/skills/delegate-grill-with-docs
```

安装后重启 Codex 以加载新 skill。

## 示例提示词

```text
针对 @xxx-doc.md，使用 $delegate-grill-with-docs 进行一次深入讨论，并把最终结论和必要修改回写到原文档。
```

```text
围绕 @xxx-doc.md，使用 $delegate-grill-with-docs 组织一次 grill-with-docs 式讨论，保留原有结构，尽量最小改动。
```

## 注意事项

- 仅在您希望 Codex 将讨论委托给某个子代理时才使用此技能。
- 它不会仅仅因为提到了 `grill-with-docs` 就自动触发。



![认可linux.do](https://ld.xh.do/ld-badge.svg)
