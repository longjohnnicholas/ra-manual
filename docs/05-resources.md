# Resources & Useful Links

## Official Claude Code Documentation

- [Claude Code Overview](https://code.claude.com/docs/en/overview) — the primary reference
- [Best Practices](https://code.claude.com/docs/en/best-practices) — Anthropic's own workflow recommendations
- [CLAUDE.md and Memory](https://code.claude.com/docs/en/memory) — how Claude reads project context
- [Sub-Agents](https://code.claude.com/docs/en/sub-agents) — creating and using custom agents
- [Skills](https://code.claude.com/docs/en/skills) — building reusable skill modules
- [VS Code Extension](https://code.claude.com/docs/en/vs-code) — IDE-specific setup and features

## Economics-Specific Skills and Workflows

These are repositories and tools built by economists, for economists.

- [Awesome Econ AI Stuff](https://github.com/meleantonio/awesome-econ-ai-stuff) — curated collection of AI skills for economics research. Includes skills for panel data analysis (Python), difference-in-differences (R), Stata regressions with publication-ready tables, and publication-quality charts. Works with Claude Code, Cursor, and other AI tools.

- [Pedro Sant'Anna's Claude Code Workflow](https://github.com/pedrohcgs/claude-code-my-workflow) — ready-to-fork Claude Code template for academics using LaTeX/Beamer + R. Features multi-agent review with specialized proofreader, slide-auditor, pedagogy-reviewer, R-reviewer, and TikZ-reviewer agents. Used to produce 6 PhD lecture decks with 800+ slides at Emory.

- [Scott Cunningham's MixtapeTools](https://github.com/scunning1975/MixtapeTools) — tools for coding, teaching, and presentations with AI assistance, focused on causal inference. By the author of *Causal Inference: The Mixtape*.

- [Stata MCP Server](https://github.com/hanlulong/stata-mcp) — Model Context Protocol server that lets Claude execute Stata commands, run `.do` files, and interpret output directly from VS Code.

## Compound Engineering

- [Compound Engineering: How Every Codes With Agents](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents) — the article that introduced the compound engineering framework: plan → execute → review → compound.

## Guides and Tutorials

- [Claude Code for Scientists](https://www.neuroai.science/p/claude-code-for-scientists) — practical guide by Patrick Mineault on using Claude Code in academic research
- [Getting Started with Claude Code for Data Scientists](https://www.dataquest.io/blog/getting-started-with-claude-code-for-data-scientists/) — data-focused tutorial with examples
- [Writing a Good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) — practical guide to crafting effective project context files
- [How Anthropic Teams Use Claude Code](https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf) (PDF) — internal workflows from Anthropic's own teams

## Related RA Manuals

- [Gentzkow & Shapiro RA Manual](https://github.com/gslab-econ/ra-manual/wiki) — the gold standard for research project organization in economics
- [mgechter RA Manual](https://github.com/mgechter/ra-manual/wiki) — coding principles that informed this manual

## Skills Collections

- [Awesome Claude Skills](https://github.com/travisvn/awesome-claude-skills) — curated list of Claude Code skills across domains
- [VoltAgent Awesome Agent Skills](https://github.com/VoltAgent/awesome-agent-skills) — 300+ skills for various use cases
- [Trail of Bits Claude Code Config](https://github.com/trailofbits/claude-code-config) — opinionated defaults, documentation, and workflows

## Quick Reference

Common Claude Code commands you'll use frequently:

| Command | What it does |
|---------|-------------|
| `claude` | Start Claude Code in the terminal |
| `/init` | Auto-generate a starter CLAUDE.md |
| `/plan` | Enter plan mode |
| `Shift+Tab` | Cycle permission modes (normal → auto → plan) |
| `/compact` | Compress conversation to free up context |
| `/clear` | Clear the conversation |
| `Ctrl+C` | Cancel current Claude action |

## Future Extensions

This manual currently focuses on Claude Code with a paid Anthropic subscription. Planned additions include:

- **Free/open-source alternatives**: Instructions for using open-weight models (e.g., via Ollama or LM Studio) as a substitute when Claude access isn't available
- **Language-specific guides**: Dedicated pages for Stata, R, Python, and MATLAB workflows with Claude
- **Advanced topics**: Custom MCP servers, CI/CD integration, automated testing pipelines
- **Data security**: Guidelines for working with sensitive or restricted-use data alongside AI tools
