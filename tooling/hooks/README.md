# Hooks

Lifecycle hooks as a **cross-harness concept** — the general idea of intercepting an agent's loop to format, guard, gate, or inject context.

**In scope:** hook ideas and patterns that are not tied to one harness's event names or config format.

**Out of scope:** anything Claude-Code-specific — its hook events (PreToolUse, PostToolUse, Stop, SessionStart, …), `settings.json` wiring, and script recipes all live under [../harnesses/claude-code/](../harnesses/claude-code/). In practice almost all hook material today is harness-specific and belongs there; this folder stays empty until a genuinely portable pattern emerges.
