---
title: Encode repeated multi-step prompts as a skill — e.g. a PR-description generator
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, skills, workflow]
source: claude-code-pro-playbook.md (Pattern 11)
---

## Takeaway

When you keep retyping the same multi-step prompt (PRs, migrations, releases), encode it once as a skill and invoke it with a slash command forever. The skill carries the exact steps and output structure so results are consistent.

## When it applies

Any workflow you've run from scratch more than twice. Mark `user-invocable: true` and give an `argument-hint` for ones people trigger directly.

## Why

A skill turns tribal multi-step prompts into a versioned, shareable artifact. The structure lives in the repo, not in each person's memory, so every invocation produces the same shape.

## Example

```markdown
# .claude/skills/create-pr/SKILL.md
---
name: create-pr
description: Generate a complete PR description for the current branch changes.
user-invocable: true
argument-hint: "[optional: additional context about the PR]"
---
1. git diff main...HEAD --stat   2. git log main...HEAD --oneline   3. read changed files
Then write: ## What / ## Why / ## How / ## Testing / ## Checklist. Output markdown only, no preamble.
```

Invoke: `/create-pr PAY-891 Stripe webhook handler` → reads the diff, emits a full description; the ticket number flows into context.

## Notes

- A Claude Code skill (`SKILL.md` + frontmatter, `user-invocable`, `argument-hint`). Genuinely cross-harness skill-authoring concepts, if any arise, live in [../../../skills/](../../../skills/).
