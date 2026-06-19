---
title: --allowedTools is the only hard enforcement boundary, not CLAUDE.md
type: pattern
confidence: proven
date: 2026-06-18
model:
version: Claude Code (headless / -p)
tags: [claude-code, security, headless, enforcement]
source: claude-code-staff-engineer-patterns.md (Patterns 7 & 8)
---

## Takeaway

CLAUDE.md constraints are advisory (~70–80% honored). `--allowedTools` is mechanical: Claude literally cannot call a tool that isn't on the list, regardless of the prompt. This — not prose — is the actual enforcement mechanism for autonomous runs.

## When it applies

Every headless/agentic run, especially any with access to production credentials. Make the allowlist as narrow as the task permits.

## Why

A prompt-level "don't touch files" can be argued around; a tool absent from the whitelist cannot fire. Scoping by capability (and by path, e.g. `Read(src/**)`) converts intent into a boundary the model can't cross.

## Example

```bash
# read-only analysis — cannot write no matter the prompt
claude -p "Analyze security vulns in src/" --allowedTools "Read,Grep,Glob,Bash(find:*)"

# controlled fix — can edit, cannot run arbitrary shell
claude -p "Fix all TS type errors" --allowedTools "Read,Write,Edit,Bash(pnpm build:*),Bash(pnpm lint:*)"

# audit that cannot install, modify, or push
claude -p "Audit deps for CVEs → JSON by severity" --bare --output-format json \
  --allowedTools "Read,Glob,Bash(npm audit:*),Bash(pnpm audit:*)" --max-turns 10
```

## Notes

- Never use `--dangerously-skip-permissions` anywhere with production-credential access; confine it to isolated containers with no network egress beyond the Anthropic API.
- The hard tier of the ENFORCEMENT layer in [[enforcement-layer-cake]]; complements [[pretooluse-input-modification]] and [[prompt-injection-sanitizing-hook]]. Drives the safe execution in [[headless-mode-ci-primitive]].
