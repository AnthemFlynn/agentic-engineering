---
title: Antigravity — an agentic IDE with a large bundled skills registry
type: reference
confidence: anecdotal
date: 2026-06-18
model:
version:
tags: [harness, antigravity, ide, skills]
source: claude-code-mastery-v3_2.html (S5)
---

## Takeaway

Antigravity is an agentic IDE/harness. It ships with a large curated registry of agentic skills (1,234+) in the universal `SKILL.md` format, installable whole or by role bundle (Web Wizard, Backend, Full-Stack, DevOps).

## When it applies

When evaluating harnesses beyond Claude Code, or when you want a big pre-built skill library in the portable SKILL.md format that also runs in other harnesses (Claude Code, Cursor, Gemini CLI, Codex).

## Example

```bash
npx antigravity-awesome-skills --claude            # install the full library
npx antigravity-awesome-skills --bundle web-wizard # role bundle: frontend-design, api-design, create-pr, …
npx antigravity-awesome-skills --bundle backend    # api-design, database-patterns, security-review, test-coverage
npx skills list                                    # list installed
```

## Notes

- The skills themselves use the cross-harness `SKILL.md` format — see [../../skills/](../../skills/) for the skill concept and [../claude-code/](../claude-code/) for Claude-Code-specific skill mechanics.
- Skill count is point-in-time (May 2026); verify before citing.
