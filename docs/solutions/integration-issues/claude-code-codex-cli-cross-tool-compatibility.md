---
title: "Cross-Tool Compatibility: Claude Code and Codex CLI"
date: 2026-02-18
category: integration-issues
tags:
  - mcp
  - codex-cli
  - claude-code
  - cross-tool
  - connected-tools
  - agents-md
severity: medium
components:
  - docs/06-connected-tools.md
  - docs/03-workflow.md
  - docs/01-setup.md
  - docs/index.md
---

# Cross-Tool Compatibility: Claude Code and Codex CLI

## Problem Statement

When refactoring the RA Manual to support both Claude Code and Codex CLI equally, we incorrectly assumed Codex CLI does NOT support MCP (Model Context Protocol) connectors. This led to publishing a wrong "Claude Code only" note on the connected tools page — telling Codex CLI users to skip the entire page.

**Symptoms:**
- Incorrect "Claude Code only" info box on `docs/06-connected-tools.md`
- Missing MCP setup guidance for Codex CLI users
- Incomplete cross-tool compatibility guidance across the manual

## Root Cause

Three factors:

1. **Feature association bias** — MCP was originally an Anthropic initiative, creating a false mental link to Claude Code exclusivity
2. **One-sided research** — We verified Claude Code capabilities thoroughly but assumed Codex CLI differences without checking official docs
3. **No verification before publishing** — The "Claude Code only" claim was added without searching Codex CLI documentation first

## Investigation Steps

1. Initial refactor correctly identified file compatibility differences (CLAUDE.md vs AGENTS.md) — this was well-researched
2. Review agents flagged `06-connected-tools.md` as entirely Claude Code-specific — we added a wrong "Claude Code only" info box
3. User challenged the assumption after checking online
4. Web search confirmed Codex CLI supports MCP via `config.toml` and `codex mcp add`
5. Official docs at https://developers.openai.com/codex/mcp/ confirmed full MCP support

## Working Solution

### Cross-Tool Compatibility Reference

| Feature | Claude Code | Codex CLI | Portable? |
|---|---|---|---|
| Context file | `CLAUDE.md` only | `AGENTS.md` only | Use `@AGENTS.md` import in CLAUDE.md |
| Skills (SKILL.md) | `.claude/skills/` | `.agents/skills/` | Same format, symlink or copy dirs |
| Custom agents | `.claude/agents/*.md` | No equivalent | Claude Code only |
| MCP connectors | JSON config | `config.toml` + `codex mcp add` | Same MCP servers work in both |
| Plan mode | `Shift+Tab` / `/plan` | Auto / Read-only / Full Access | Both support it |
| VS Code extension | "Claude Code" by Anthropic | "ChatGPT" by OpenAI | Both available |

### MCP Configuration: Claude Code vs Codex CLI

**Claude Code** — add to Claude Code settings (JSON):
```json
{
  "mcpServers": {
    "google-drive": {
      "command": "npx",
      "args": ["-y", "@anthropic/google-drive-mcp"]
    }
  }
}
```

**Codex CLI** — add to `~/.codex/config.toml` (TOML):
```toml
[mcp_servers.google-drive]
command = "npx"
args = ["-y", "@anthropic/google-drive-mcp"]
```

Or use the CLI:
```bash
codex mcp add google-drive -- npx -y @anthropic/google-drive-mcp
```

### Context File Cross-Tool Pattern

For teams using both Claude Code and Codex CLI on the same repo:

1. Write all shared instructions in `AGENTS.md` (the open standard)
2. Create a `CLAUDE.md` that imports it: `@AGENTS.md`
3. Add Claude-specific instructions below the import line

Do NOT use symlinks — they fail silently on Windows.

## Prevention Strategies

### Always verify both sides

Before documenting any tool as lacking a feature:
- Check the official docs for THAT tool specifically
- Search release notes — features get added frequently
- Only claim exclusivity if the other tool's docs explicitly confirm non-support

### Canonical verification links

| Tool | MCP docs | Config docs |
|---|---|---|
| Claude Code | https://code.claude.com/docs/en/mcp | Claude Code settings |
| Codex CLI | https://developers.openai.com/codex/mcp/ | https://developers.openai.com/codex/config-reference/ |

### Language precision

- Avoid: "Codex CLI doesn't support X"
- Prefer: "As of [date], verify X support in [official docs link]"
- Only mark features as tool-exclusive after checking both sides

### Features that genuinely differ (verified)

These are real differences, not assumptions:
- Context file names: `CLAUDE.md` vs `AGENTS.md` (confirmed in both docs)
- Custom agents directory: `.claude/agents/` exists, no Codex equivalent (confirmed)
- Config format: JSON (Claude Code) vs TOML (Codex CLI) (confirmed)

## Related Documentation

- `docs/06-connected-tools.md` — MCP connector setup (updated to be tool-agnostic)
- `docs/03-workflow.md` — Cross-tool file format compatibility
- `docs/01-setup.md` — Installation for both tools
- `docs/plans/2026-02-18-refactor-setup-page-claude-code-codex-plan.md` — Refactoring plan

## References

- [Codex CLI MCP docs](https://developers.openai.com/codex/mcp/)
- [Codex CLI config reference](https://developers.openai.com/codex/config-reference/)
- [Claude Code MCP docs](https://code.claude.com/docs/en/mcp)
- [AGENTS.md open standard (AAIF)](https://aaif.io/)
- [Agent Skills specification](https://agentskills.io/specification)
