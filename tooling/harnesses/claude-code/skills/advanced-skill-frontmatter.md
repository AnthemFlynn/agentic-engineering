---
title: Advanced skill frontmatter — once, fork, scoped hooks, auto-trigger
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, skills]
source: claude-code-mastery-v3_2.html (Level 2, P4)
---

## Takeaway

Four skill-frontmatter fields most developers never use:

- **`once: true`** — body runs only once per session; later invocations are no-ops. Ideal for expensive setup (loading architecture/schema docs).
- **`context: fork`** — runs in a forked subagent context; the skill's verbose processing stays isolated, main context sees only the result.
- **`hooks:`** — hooks scoped to the skill's lifecycle only. A PreToolUse hook inside a skill fires only for that skill's tool calls, not the whole session.
- **Description precision** — the auto-trigger signal. "Use when the user asks to review code, after writing new code, or mentions a PR review" triggers reliably; "code review stuff" never does.

## When it applies

`once` for one-time loads; `fork` when the skill does noisy processing; scoped `hooks` for skill-local enforcement (e.g. a secure-ops skill that runs a security check before every bash command); precise descriptions always.

## Example

```yaml
---
name: load-architecture
description: Load and internalize project architecture docs. Use at session start
  and whenever architecture context is needed.
once: true
---
Read docs/architecture.md, docs/domain-model.md, docs/adr/. Summarize in 3 bullets, then confirm ready.
```

## Notes

- `context: fork` is the skill-level expression of [[context-focus-beats-parallelism]]; sits at the "skills" tier of [[skills-subagents-agent-teams-spectrum]]. Basic skill structure: [[create-pr-skill]].
