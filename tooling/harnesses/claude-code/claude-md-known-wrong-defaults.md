---
title: A copy-paste "known wrong defaults" block for CLAUDE.md
type: reference
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, claude-md]
source: claude-code-pro-playbook.md (Anti-Patterns section)
---

## Takeaway

A reusable CLAUDE.md section that pre-empts the defaults Claude reaches for without explicit rules. Adopt the lines that match your stack; each is one class of mistake you won't have to correct in-session.

## When it applies

Add at project setup, then grow it via the correction loop in [[claude-md-living-document]]. The exact rules are stack-specific — the categories generalize.

## Example

```markdown
## Known wrong defaults (correct these immediately)

### Package manager
ALWAYS use pnpm. NEVER use npm or yarn.

### Testing
Run ONLY the affected test file: `pnpm test [file]`. Full suite only when asked.

### Database
NEVER run migrations against production. Migration command: `pnpm db:migrate` (local only).

### Git
NEVER `git push --force`. Use `--force-with-lease`. Commits follow conventional commits.

### File creation
NEVER create a file without checking if the pattern already exists (check src/services/ first).

### Error handling
NEVER throw plain Error. Import from src/errors/index.ts (ValidationError, NotFoundError, …).

### Logging
NEVER console.log — use logger from src/lib/logger.ts. NEVER log bodies, tokens, or PII.
```

## Notes

- These are advisory (~70–80% honored). For rules that must always hold (no `.env` reads, no destructive bash), enforce mechanically — see [[block-destructive-bash]], [[protect-sensitive-files]], [[allowed-tools-hard-contract]].
