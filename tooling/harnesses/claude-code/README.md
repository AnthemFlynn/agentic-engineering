# Claude Code

Anthropic's agentic coding harness — CLI, desktop, web, and IDE extensions.

**In scope:** everything Claude-Code-specific — settings & permissions, hooks, subagents, slash commands, skills, CLAUDE.md, session/CI workflows, and the runtime/SDK layer. If it only makes sense inside the Claude Code / Claude platform family, it lives here.

**Out of scope:** only *genuinely universal / cross-harness* material belongs in the top-level [../../hooks/](../../hooks/), [../../skills/](../../skills/), [../../mcps/](../../mcps/), [../../plugins/](../../plugins/), and [../../clis/](../../clis/) categories. When in doubt, it's Claude-Code-specific — put it here.

Notes are organized into subfolders by artifact type. This file is the index.

## Getting started & mindset — [`getting-started/`](getting-started/)
- [Team quickstart (4 steps)](getting-started/team-quickstart.md)
- [Compound engineering loop (correction → hook → skill)](getting-started/compound-engineering-loop.md)

## CLAUDE.md — [`claude-md/`](claude-md/)
- [Living document + correction loop](claude-md/claude-md-living-document.md)
- [Known wrong-defaults block](claude-md/claude-md-known-wrong-defaults.md)
- [Diagnostic prompt → root cause into CLAUDE.md](claude-md/diagnostic-prompt-to-claude-md.md)

## Hooks — [`hooks/`](hooks/)
- [Auto-format on write (PostToolUse)](hooks/auto-format-on-write.md)
- [Block destructive bash (PreToolUse, exit 2)](hooks/block-destructive-bash.md)
- [Protect sensitive files (PreToolUse path guard)](hooks/protect-sensitive-files.md)
- [Test-gate on stop (Stop hook + loop guard)](hooks/test-gate-on-stop.md)
- [Session-start context injection](hooks/session-start-context-injection.md)
- [PreCompact / PostCompact backup + re-inject](hooks/precompact-postcompact-backup.md)
- [PreToolUse input modification (transparent rewrite)](hooks/pretooluse-input-modification.md)
- [Prompt-injection sanitizing hook](hooks/prompt-injection-sanitizing-hook.md)
- [Five hook handler types (command/prompt/agent/http/mcp_tool)](hooks/hook-handler-types.md)
- [SubagentStop quality gates](hooks/subagentstop-quality-gates.md)
- [Async hooks (async: true)](hooks/async-hooks.md)
- [Debugging hooks when they don't fire](hooks/debugging-hooks.md)

## Subagents & forks — [`subagents/`](subagents/)
- [codebase-explorer (research without context pollution)](subagents/subagent-codebase-explorer.md)
- [code-reviewer (adversarial, CLAUDE.md-gated)](subagents/subagent-code-reviewer.md)
- [Forks vs subagents](subagents/forks-vs-subagents.md)

## Commands & skills — [`commands/`](commands/) · [`skills/`](skills/)
- [/plan as a spec generator](commands/plan-command-as-spec.md)
- [Encode repeated workflows as a skill (create-pr)](skills/create-pr-skill.md)
- [Advanced skill frontmatter (once / fork / scoped hooks)](skills/advanced-skill-frontmatter.md)

## Session & CI workflows — [`workflows/`](workflows/)
- [Spec-driven workflow (plan mode → execute)](workflows/spec-driven-workflow.md)
- [Writer/reviewer loop (fresh-context review)](workflows/writer-reviewer-loop.md)
- [Worktrees for parallel features](workflows/worktrees-parallel-features.md)
- [Vertical-slice prompt](workflows/vertical-slice-prompt.md)
- [Headless mode as a CI primitive](workflows/headless-mode-ci-primitive.md)

## Config & enforcement — [`config/`](config/)
- [Committed settings.json baseline (permissions + hooks)](config/committed-settings-json-baseline.md)
- [`--allowedTools` as a hard contract](config/allowed-tools-hard-contract.md)
- [`auto` permission mode for CI](config/auto-permission-mode-for-ci.md)

## Build · runtime — [`build/`](build/)
*Below [the line](build/the-line.md): your application drives the agent loop.*
- [Agent SDK — budgeted run with model routing](build/agent-sdk-budgeted-run.md)
- [MCP server design — intent-grouped tools](build/mcp-server-intent-grouped-design.md)
- [Prompt caching — static first, dynamic last](build/prompt-caching.md)
- [Durable execution with phase checkpoints](build/durable-execution-checkpoints.md)
- [Governance — audit, shadow-MCP, hard boundaries](build/governance-audit-shadow-mcp.md)
