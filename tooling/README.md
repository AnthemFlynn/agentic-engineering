# Tooling

The concrete platforms and CLIs used to build and run agents, organized by tool category.

A technique belongs here only when it is genuinely tied to a specific tool — vendor-neutral design ideas go in their concept area ([harness-design/](../harness-design/), [orchestration/](../orchestration/), etc.).

## Categories

| Folder | What lives here |
|--------|-----------------|
| [harnesses/](harnesses/) | Full agentic harnesses that run the agent loop — Claude Code, OpenCode, Codex. |
| [clis/](clis/) | Standalone command-line tools agents drive or depend on. |
| [mcps/](mcps/) | Model Context Protocol servers — setup, configuration, gotchas. |
| [skills/](skills/) | Agent skills — authoring, structure, discovery, distribution. |
| [hooks/](hooks/) | Lifecycle hooks (PreToolUse, PostToolUse, Stop, …) and what to wire them to. |
