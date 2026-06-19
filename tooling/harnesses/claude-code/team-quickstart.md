---
title: A four-step Claude Code quickstart for teams
type: playbook
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, onboarding, team]
source: claude-code-field-guide-may2026.md (Quickstart)
---

## Takeaway

A team new to Claude Code gets a better foundation than most have after months by doing exactly four things, in order — each committed to the repo so everyone inherits it.

## When it applies

Onboarding a team or a new repo to a Claude Code practice. Do these before anything fancier; everything else builds on top.

## Example

1. **Run `/init`** in each active repo; curate the output down to ~100 lines. Commit it. → [[claude-md-living-document]]
2. **Add one PreToolUse hook** that blocks `rm -rf` and `DROP TABLE`. Commit it. → [[block-destructive-bash]]
3. **Add one PostToolUse hook** that runs your formatter after every edit. Commit it. → [[auto-format-on-write]]
4. **Write one skill** for the workflow you re-explain most (PR format, test conventions, migration pattern). → [[create-pr-skill]]

## Notes

- Maps to the rollout order in [[skills-subagents-agent-teams-spectrum]] (rules → enforcement → procedures), then graduate to [[committed-settings-json-baseline]] and the [[spec-driven-workflow]].
