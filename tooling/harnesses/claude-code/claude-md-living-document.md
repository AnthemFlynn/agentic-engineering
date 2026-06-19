---
title: Curate CLAUDE.md as a living document, fed by a correction loop
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, claude-md, context]
source: claude-code-pro-playbook.md (Pattern 1)
---

## Takeaway

CLAUDE.md should be **curated, not comprehensive**. The maintenance mechanism is a correction loop: when Claude makes a wrong assumption, don't just fix the output — add the correction to CLAUDE.md immediately, commit it, and the whole team inherits the fix.

## When it applies

Any project Claude works on repeatedly. The payoff compounds with team size and project age — each captured correction is one mistake no teammate's session repeats.

## Why

A write-once CLAUDE.md rots and gets half-ignored. A file that grows by one targeted rule each time Claude gets something wrong stays dense with *only* the corrections that matter, instead of aspirational documentation nobody verified.

## Example

The highest-value section is an explicit list of what Claude gets wrong without guidance:

```markdown
## Things Claude gets wrong without this
- Running `npm test` instead of `pnpm test` — use pnpm
- Importing from `@company/utils` (deprecated) — use `@company/core`
- Adding try/catch around Drizzle queries — error middleware handles that
- Using `console.log` — use `logger.debug()` from src/lib/logger
```

The correction loop in practice: when Claude writes `npm test` a third time → "Add to CLAUDE.md: this project uses pnpm, not npm. Always use pnpm." Claude edits the file; you commit it.

## Notes

- Keep the canonical wrong-defaults block as [[claude-md-known-wrong-defaults]].
- When a correction doesn't stick after repeating, escalate with the [[diagnostic-prompt-to-claude-md]].
- For splitting a large file by task relevance, see [[compound-claude-md-dynamic-import]]. CLAUDE.md is the BEHAVIORAL layer of the [[enforcement-layer-cake]] — advisory; back hard rules with enforcement controls.
