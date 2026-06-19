---
title: An adversarial code-reviewer subagent, gated by CLAUDE.md
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, subagents, review, security]
source: claude-code-pro-playbook.md (Pattern 8)
---

## Takeaway

Define a `code-reviewer` subagent whose job is to *find problems, not validate the work*. It diffs `HEAD`, reads each changed file, and reports CRITICAL / IMPORTANT / SUGGESTION findings with `file:line`. Make it mandatory for sensitive paths via a CLAUDE.md review gate.

## When it applies

After any implementation; required before committing payment, auth, or data-mutation code. The CLAUDE.md gate is what makes it non-optional.

## Why

Self-review approves itself. A dedicated adversarial reviewer with an explicit "find problems" framing and a severity-tiered output format produces specific, actionable findings instead of "looks good."

## Example

```markdown
# .claude/agents/code-reviewer.md
---
name: code-reviewer
description: Adversarial review after implementation; before committing payment/auth/data code.
tools: Read, Glob, Grep, Bash
model: sonnet
---
Run `git diff HEAD`, read each changed file. Evaluate security, correctness, maintainability,
performance. Output:
CRITICAL (must fix): [issue] in [file]:[line] — [why]
IMPORTANT (should fix): ...
SUGGESTION (consider): ...
If nothing critical, say so with reasoning. Vague feedback is useless.
```

Gate in CLAUDE.md: *"Before committing in src/payments/ or src/auth/: MUST invoke code-reviewer. Do not commit until all CRITICAL issues resolved."*

## Notes

- The single-session form of the [[writer-reviewer-loop]]; the fresh-context, no-author-bias rationale is [[external-grader-loop]].
