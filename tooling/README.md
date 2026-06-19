# Tooling

The concrete platforms and CLIs used to build and run agents, organized by tool category.

A technique belongs here only when it is genuinely tied to a specific tool — vendor-neutral design ideas go in their concept area ([harness-design/](../harness-design/), [orchestration/](../orchestration/), etc.).

## Categories

| Folder | What lives here |
|--------|-----------------|
| [harnesses/](harnesses/) | Full agentic harnesses that run the agent loop — Claude Code, OpenCode, Codex, Antigravity. **Harness-specific material (hooks, skills, settings, subagents) lives under its harness**, e.g. [harnesses/claude-code/](harnesses/claude-code/). |
| [plugins/](plugins/) | Workflow plugins — installable bundles of skills/commands/hooks (Superpowers, BMAD). |
| [clis/](clis/) | Standalone command-line tools agents drive or depend on. |
| [mcps/](mcps/) | Model Context Protocol servers — cross-harness concepts (a server's own setup isn't tied to one harness). |
| [skills/](skills/) | Skills as a *cross-harness* concept only. Harness-specific skill recipes (e.g. Claude Code `SKILL.md`) go under that harness. |
| [hooks/](hooks/) | Hooks as a *cross-harness* concept only. Harness-specific hook configs (e.g. Claude Code `settings.json`) go under that harness. |
