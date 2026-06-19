---
title: Use `auto` permission mode for unattended/CI runs
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code v2.1.x
tags: [claude-code, permissions, ci, security]
source: claude-code-field-guide-may2026.md (section 9)
---

## Takeaway

For unattended or CI runs, `auto` permission mode puts a classifier model in front of commands: it reviews each before execution, blocking scope escalation and hostile-content-driven actions while letting routine work proceed without prompts. If it repeatedly blocks actions in non-interactive mode, the run aborts rather than proceeding blind.

## When it applies

Headless/CI contexts where no human is present to answer permission prompts, but you still want a judgment layer beyond a static allowlist. Pair with — don't replace — a tight `--allowedTools` boundary.

## Why

A static allowlist can't reason about *intent* (a command may be on the list but used to escalate). The classifier adds a per-command judgment pass; the abort-on-repeated-block behavior fails safe instead of grinding forward when something is clearly wrong.

## Notes

- Complements the hard boundary of [[allowed-tools-hard-contract]] and the committed [[committed-settings-json-baseline]] permissions; use together in [[headless-mode-ci-primitive]] runs.
- Never substitute `auto` for `--dangerously-skip-permissions` in production-credentialed environments.
