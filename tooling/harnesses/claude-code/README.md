# Claude Code

Anthropic's agentic coding harness — CLI, desktop, web, and IDE extensions.

**In scope:** Claude-Code-as-a-harness — settings, slash commands, subagents, session/context behavior, and version-specific quirks.

For a sub-system that exists across harnesses, prefer the dedicated category and keep only the Claude-Code-specific plumbing here: skill authoring → [../../skills/](../../skills/), hook recipes → [../../hooks/](../../hooks/), MCP wiring → [../../mcps/](../../mcps/).

## Notes

**CLAUDE.md**
- [Living document + correction loop](claude-md-living-document.md)
- [Known wrong-defaults block](claude-md-known-wrong-defaults.md)
- [Diagnostic prompt → root cause into CLAUDE.md](diagnostic-prompt-to-claude-md.md)

**Config & enforcement**
- [Committed settings.json baseline (permissions + hooks)](committed-settings-json-baseline.md)
- [`--allowedTools` as a hard contract](allowed-tools-hard-contract.md)

**Subagents**
- [codebase-explorer (research without context pollution)](subagent-codebase-explorer.md)
- [code-reviewer (adversarial, CLAUDE.md-gated)](subagent-code-reviewer.md)

**Commands**
- [/plan as a spec generator](plan-command-as-spec.md)

**Session workflows**
- [Writer/reviewer loop (fresh-context review)](writer-reviewer-loop.md)
- [Worktrees for parallel features](worktrees-parallel-features.md)
- [Vertical-slice prompt](vertical-slice-prompt.md)
- [Headless mode as a CI primitive](headless-mode-ci-primitive.md)
