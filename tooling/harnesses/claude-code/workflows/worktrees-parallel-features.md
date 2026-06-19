---
title: Run parallel Claude sessions with git worktrees, one branch each
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, worktrees, parallelism, workflow]
source: claude-code-pro-playbook.md (Pattern 5); claude-code-field-guide-may2026.md (section 7)
---

## Takeaway

Give each independent task its own git worktree, branch, and Claude session in a separate terminal. Each session has its own CLAUDE.md view and history and physically cannot touch another's files. Review diffs as they finish; merge sequentially.

## When it applies

Several *independent* tickets you'd otherwise sequence (e.g. three standup tickets that don't share files). Not for interdependent work or same-file edits — merge conflicts and coordination erase the gain.

## Why

The isolation is filesystem-level, not advisory: separate working directories mean no cross-contamination of files or context. It's the manual, durable cousin of [[agent-teams-bidirectional-multi-agent]], and it banks the [[context-focus-beats-parallelism]] win.

## Example

```bash
git worktree add ../myrepo-feat-auth  feat/oauth-login
git worktree add ../myrepo-fix-deploy fix/deployment-timeout
cd ../myrepo-feat-auth && claude   # Terminal 1: scope src/auth/ only
cd ../myrepo-fix-deploy && claude  # Terminal 2: scope src/deploy/ only
# ... review diffs as each completes, then:
git worktree remove ../myrepo-feat-auth
```

Scope each session explicitly ("Scope: src/auth/ only") to keep the isolation honest. Claude Code's `-w` flag creates and manages worktrees for you.

## Notes

- Teams run **4–8 concurrent worktrees per developer** reliably as of mid-2026; above that the bottleneck is review throughput, not Claude.
- **Role discipline:** each session has one job. The moment one starts drifting into another's files, stop, commit what's safe, and reset — parallel sessions fail when they blur together.
- **Advanced pattern:** use plan mode to decompose a feature, then spawn a subagent per task with its own worktree/branch, each returning a diff to review — the closest thing to "many engineers on one feature." See [[spec-driven-workflow]].
- Workflow-level isolation; the in-process equivalent is agent teammates each in their own worktree. Clean up with `git worktree remove` when merged.
