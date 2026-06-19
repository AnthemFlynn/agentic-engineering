---
title: Write in one session, review in a fresh one
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, review, workflow]
source: claude-code-pro-playbook.md (Pattern 3)
---

## Takeaway

Claude reviewing its own just-written code almost always approves it. Split the work: session 1 implements; session 2 (fresh context, same repo) reviews adversarially. Fresh context removes author bias.

## When it applies

Before merging anything where a missed defect is costly — security, payments, auth, data mutation. Cheap enough to use routinely on non-trivial changes.

## Why

A session that wrote the code shares its blind spots and its rationalizations. A fresh session reads the diff cold and is free to push back as it would in a real PR review.

## Example

```
# Session 1 (implement)
Implement Redis-backed rate-limiting middleware in src/middleware/rateLimit.ts.
Per-user, 100 req/min default, configurable per-route. Commit when done.

# Session 2 (fresh, same repo — review)
Review the last commit as a senior engineer. Be adversarial; push back as you would in a PR.
- Security: any way to bypass/spoof the limit?
- Correctness: does the Redis key expire correctly?
- Edge cases: what if Redis is unavailable?
- Performance: N+1 calls per request?
Output specific issues with file:line.
```

## Notes

- The in-session, subagent form: [[subagent-code-reviewer]]. The rubric-scored, retrying form: [[external-grader-loop]].
