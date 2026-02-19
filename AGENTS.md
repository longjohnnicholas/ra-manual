# RA Manual — Project Context

## What this is
MkDocs Material site for research assistants on using AI coding agents.
Live at: https://ntsivanidis.github.io/ra-manual/

## Build & preview
```bash
pip install mkdocs-material
mkdocs serve          # local preview at localhost:8000
mkdocs gh-deploy      # manual deploy (auto-deploys on push to main)
```

## Site structure
```
docs/
├── index.md               # Home page
├── 01-setup.md            # VS Code + Claude Code / Codex CLI setup
├── 02-why-claude-code.md  # Why AI coding tools for research
├── 03-workflow.md         # Workflow: context files, skills, sub-agents
├── 04-code-principles.md  # Project organization & coding standards
├── 05-resources.md        # Links and references
├── 06-connected-tools.md  # MCP connectors (Drive, Gmail, WhatsApp)
├── plans/                 # Internal planning docs (not published)
└── solutions/             # Documented learnings (not published)
```

Navigation is defined in `mkdocs.yml`. Only pages listed in `nav:` are published.

## Conventions
- **Two tools, equal footing:** Claude Code and Codex CLI. Never present one as primary.
- **Tool-agnostic language:** Use "your agent" not "Claude" when the advice applies to both.
- **Tabbed content for tool differences:** Use `=== "Claude Code"` / `=== "Codex CLI"` tabs.
- **Admonitions should have titles:** Use `!!! tip "Title"` not bare `!!! tip`.
- **No hardcoded colors in HTML:** Breaks dark mode. Use CSS classes instead.
- **Grid cards pattern:** `:material-icon:{ .lg .middle } __Title__` with 4-space indent.
- **Section separators:** `---` between H2 sections only.
- **Relative paths for internal links:** `[text](01-setup.md)` not absolute URLs.

## Cross-tool compatibility (verified 2026-02-18)
| Feature | Claude Code | Codex CLI |
|---|---|---|
| Context file | CLAUDE.md | AGENTS.md |
| Skills | .claude/skills/ | .agents/skills/ |
| Custom agents | .claude/agents/ | No equivalent |
| MCP connectors | JSON config | config.toml / `codex mcp add` |
| Plan mode | Shift+Tab / /plan | Auto / Read-only / Full Access |

**Both tools support MCP.** Do not mark MCP as Claude-only.

## Gotchas
- `mkdocs.yml` site_url points to `longjohnnicholas` but README points to `ntsivanidis` — known mismatch
- Symlinks fail silently on Windows — always recommend `@AGENTS.md` import pattern instead
- `docs/plans/` and `docs/solutions/` are NOT in mkdocs.yml nav — they are internal only
- PEP 668 blocks `pip install` on macOS — use a venv for mkdocs
