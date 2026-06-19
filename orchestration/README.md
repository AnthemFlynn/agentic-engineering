# Orchestration

Wiring multiple agents — or multiple turns of one agent — into a larger system.

**In scope:** multi-agent topologies (fan-out, pipeline, DAG, judge panels), autonomous loops and their control/recovery, handoffs and shared state, worktree isolation, barriers vs. pipelines, loop-until-done and loop-until-budget patterns.

**Out of scope:** which model each step uses (→ [models/](../models/)), the tools an individual agent calls (→ [harness-design/](../harness-design/)).

## Notes

- [Agent teams — bidirectional multi-agent](agent-teams-bidirectional-multi-agent.md)
- [Context focus beats parallelism](context-focus-beats-parallelism.md)
- [Competing hypotheses with an integrator](competing-hypotheses-with-integrator.md)
- [The enforcement layer-cake](enforcement-layer-cake.md)
