# Claude Code

Anthropic's agentic coding harness — CLI, desktop, web, and IDE extensions.

**In scope:** everything Claude-Code-specific — settings & permissions, hooks, subagents, slash commands, skills, CLAUDE.md, session/CI workflows, and version-specific quirks. If it only makes sense inside Claude Code, it lives here.

**Out of scope:** only *genuinely universal / cross-harness* material belongs in the top-level [../../hooks/](../../hooks/), [../../skills/](../../skills/), [../../mcps/](../../mcps/), and [../../clis/](../../clis/) categories. When in doubt, it's Claude-Code-specific — put it here.

## Notes

**Getting started & mindset**
- [Team quickstart (4 steps)](team-quickstart.md)
- [Compound engineering loop (correction → hook → skill)](compound-engineering-loop.md)

**CLAUDE.md**
- [Living document + correction loop](claude-md-living-document.md)
- [Known wrong-defaults block](claude-md-known-wrong-defaults.md)
- [Diagnostic prompt → root cause into CLAUDE.md](diagnostic-prompt-to-claude-md.md)

**Hooks**
- [Auto-format on write (PostToolUse)](auto-format-on-write.md)
- [Block destructive bash (PreToolUse, exit 2)](block-destructive-bash.md)
- [Protect sensitive files (PreToolUse path guard)](protect-sensitive-files.md)
- [Test-gate on stop (Stop hook + loop guard)](test-gate-on-stop.md)
- [Session-start context injection](session-start-context-injection.md)
- [PreCompact / PostCompact backup + re-inject](precompact-postcompact-backup.md)
- [PreToolUse input modification (transparent rewrite)](pretooluse-input-modification.md)
- [Prompt-injection sanitizing hook](prompt-injection-sanitizing-hook.md)
- [Five hook handler types (command/prompt/agent/http/mcp_tool)](hook-handler-types.md)
- [SubagentStop quality gates](subagentstop-quality-gates.md)
- [Async hooks (async: true)](async-hooks.md)
- [Debugging hooks when they don't fire](debugging-hooks.md)

**Subagents & forks**
- [codebase-explorer (research without context pollution)](subagent-codebase-explorer.md)
- [code-reviewer (adversarial, CLAUDE.md-gated)](subagent-code-reviewer.md)
- [Forks vs subagents](forks-vs-subagents.md)

**Commands & skills**
- [/plan as a spec generator](plan-command-as-spec.md)
- [Encode repeated workflows as a skill (create-pr)](create-pr-skill.md)
- [Advanced skill frontmatter (once / fork / scoped hooks)](advanced-skill-frontmatter.md)

**Session & CI workflows**
- [Spec-driven workflow (plan mode → execute)](spec-driven-workflow.md)
- [Writer/reviewer loop (fresh-context review)](writer-reviewer-loop.md)
- [Worktrees for parallel features](worktrees-parallel-features.md)
- [Vertical-slice prompt](vertical-slice-prompt.md)
- [Headless mode as a CI primitive](headless-mode-ci-primitive.md)

**Config & enforcement**
- [Committed settings.json baseline (permissions + hooks)](committed-settings-json-baseline.md)
- [`--allowedTools` as a hard contract](allowed-tools-hard-contract.md)
- [`auto` permission mode for CI](auto-permission-mode-for-ci.md)

**Build · runtime (below [the line](the-line.md))**
- [Agent SDK — budgeted run with model routing](agent-sdk-budgeted-run.md)
- [MCP server design — intent-grouped tools](mcp-server-intent-grouped-design.md)
- [Prompt caching — static first, dynamic last](prompt-caching.md)
- [Durable execution with phase checkpoints](durable-execution-checkpoints.md)
- [Governance — audit, shadow-MCP, hard boundaries](governance-audit-shadow-mcp.md)
