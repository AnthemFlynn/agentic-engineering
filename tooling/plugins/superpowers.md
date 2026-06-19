---
title: Superpowers — an opinionated TDD SDLC shipped as a plugin
type: reference
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [plugin, superpowers, workflow, tdd]
source: claude-code-mastery-v3_2.html (E6, S1)
---

## Takeaway

Superpowers (by Jesse Vincent / obra) packages an engineering *culture* — a TDD-enforced SDLC — as a folder of markdown skills + hooks. The bet: agents lack discipline, not capability, and discipline distributes as plain text. Works unmodified across 6 runtimes (Claude Code, Cursor, Gemini CLI, GitHub Copilot CLI, Codex, OpenCode).

## When it applies

When you want a ready-made, opinionated execution workflow with TDD as a hard gate rather than assembling your own skills. Accepted into Anthropic's official plugin marketplace (Jan 2026).

## Example

```bash
/plugin install superpowers@obra      # or: npx skills add obra/superpowers
/brainstorm     # structured idea → spec via questions
/write-plan     # spec → ordered task list with tests
/execute-plan   # fresh subagent per task; implement → test → review → merge
```

A session-start hook injects a <2,000-token bootstrap telling Claude to check for relevant skills before each task. TDD is non-negotiable: the skill deletes any code written before a failing test exists (RED → GREEN → REFACTOR).

## Notes

- A concrete, packaged instance of the [[spec-driven-workflow]] and the [[skills-subagents-agent-teams-spectrum]] (it lives at the "skills" tier but coordinates subagents per task).
- Pairs with [[bmad]] (design/spec phase) for full-SDLC coverage. Star counts/marketplace status are point-in-time (May 2026) — verify before citing.
