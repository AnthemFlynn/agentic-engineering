---
title: Write the success criteria before the code so the agent self-verifies
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [prompting, rubric]
source: claude-code-staff-engineer-patterns.md (Pattern 9)
---

## Takeaway

Give an explicit "DONE means ALL of the following are true" checklist *in the prompt, before implementation*. The agent uses it as its own self-verification gate instead of declaring done when it subjectively feels finished. This is the single highest-leverage prompt change for complex implementations.

## When it applies

Any non-trivial implementation task. The more a task has a verifiable definition of done (tests pass, build clean, specific behaviors), the bigger the payoff. Less useful for open-ended exploration with no crisp success state.

## Why

Without criteria, the model picks its own "done" and stops early. A concrete checklist turns vague intent into runnable checks the agent will actually execute (run the suite, check the build, test the failover) before claiming completion.

## Example

```
Implement the rate limiter. DONE means ALL are true:
[ ] pnpm test src/middleware/rateLimit.test.ts passes, 0 failures
[ ] pnpm build exits 0, no TS errors
[ ] Redis failure degrades gracefully to in-memory fallback (test: kill Redis mid-request)
[ ] Every response sets X-RateLimit-Limit/Remaining/Reset
[ ] Per-user limit configurable per-route, not just globally
[ ] No hardcoded secrets — all from environment
Do not declare done until every box checks. Fix a failing box before moving on.
```

## Notes

- Self-check by the author; pair with an independent [[external-grader-loop]] when the bar is high.
- For CI, have the agent emit the checklist result as a [[structured-output-contract]].
