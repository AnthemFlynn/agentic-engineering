# Harnesses

Full agentic harnesses — the runtimes that drive the agent loop: read context, call tools, observe results, repeat.

**In scope:** harness-specific setup, configuration, capabilities, quirks, and version-sensitive behavior. One subfolder per harness:

| Folder | Harness |
|--------|---------|
| [claude-code/](claude-code/) | Anthropic's Claude Code (CLI, desktop, web, IDE). |
| [opencode/](opencode/) | OpenCode. |
| [codex/](codex/) | OpenAI Codex CLI. |

**Out of scope:** vendor-neutral loop design (→ [../../orchestration/](../../orchestration/)) and tool/observation design (→ [../../harness-design/](../../harness-design/)).
