---
title: Durable execution — idempotent phase checkpoints that survive interruption
type: pattern
confidence: proven
date: 2026-06-18
model:
version:
tags: [claude-code, agent-sdk, durability, runtime]
source: claude-code-mastery-v3_2.html (Level 4, P4)
---

## Takeaway

Standard agent runs fail silently on timeout, network error, or context overflow — losing all completed work. Durable execution checkpoints each completed phase to disk so a re-run resumes from the last success, not the beginning. The critical property: **each phase must be idempotent** — running it twice equals running it once.

## When it applies

Long-running multi-phase tasks (migrations, large generations, multi-step pipelines) where partial progress is expensive to lose and a failure mid-run is likely. Persist the SDK `sessionId` in the checkpoint to carry agent state across resumptions.

## Why

Idempotency is what makes retry safe — without it, re-running a phase risks duplicate records, double sends, or inconsistent state. With a checkpoint file plus idempotent phases, "re-run the same command" is a safe resume.

## Example

```ts
let ckpt = exists(CKPT) ? read(CKPT) : { completedPhases: [], sessionId: undefined };
for (const phase of phases) {
  if (ckpt.completedPhases.includes(phase.id)) continue;     // skip completed
  const result = await runPhase(phase, ckpt.sessionId);
  ckpt.sessionId ??= result.sessionId;                        // persist for resumption
  ckpt.completedPhases.push(phase.id); write(CKPT, ckpt);
}
unlink(CKPT);                                                 // clean up on success
```

## Notes

- Built on [[agent-sdk-budgeted-run]] (session resumption). The plan-as-phases shape mirrors [[spec-driven-workflow]]. Below [[the-line]].
