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

- [Pedro Sant'Anna's Claude Code Workflow](https://psantanna.com/claude-code-my-workflow/) — comprehensive starter kit for academics using Claude Code with LaTeX/Beamer, R, and Quarto. Features 10 specialized review agents, 19 slash commands, pipeline conversion (Beamer→Quarto, TikZ→SVG), and quality gates. Extracted from a PhD economics course at Emory (6 lectures, 800+ slides). [GitHub repo](https://github.com/pedrohcgs/claude-code-my-workflow).

## Compound Engineering

- [Compound Engineering: How Every Codes With Agents](https://every.to/chain-of-thought/compound-engineering-how-every-codes-with-agents) — the article that introduced the compound engineering framework: plan → execute → review → compound.
- [Compound Engineering: The Definitive Guide](https://every.to/source-code/compound-engineering-the-definitive-guide) — comprehensive guide to the methodology.
- [Compound Engineering Plugin](https://github.com/EveryInc/compound-engineering-plugin) — open-source plugin with 29 agents, 22 commands, and 19 skills. Works with Claude Code. See [installation instructions](03-workflow.md#installing-in-claude-code).

## Guides and Tutorials

- [Anthropic's Prompt Engineering Interactive Tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial) — hands-on course covering prompt structure, chain-of-thought reasoning, avoiding hallucinations, and building complex prompts. Available as Jupyter notebooks or Google Sheets.
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

## Voice-to-Text Tools

Speaking is 3x faster than typing (~150 wpm vs ~50 wpm). These tools let you dictate prompts and code comments:

- [Wispr Flow](https://www.wispr.ai/) — AI-powered dictation for Mac. Learns your vocabulary and coding terms. Recommended.
- [macOS Dictation](https://support.apple.com/guide/mac-help/use-dictation-mh40584/mac) — Built-in, free. Press `Fn Fn` to activate.
- [Windows Speech Recognition](https://support.microsoft.com/en-us/windows/use-voice-typing-to-talk-instead-of-type-on-your-pc-fec94565-c4bd-329d-e59a-af033fa5689f) — Built-in Windows feature.

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

This manual covers Claude Code and Codex CLI. Planned additions include:

- **Free/open-source alternatives**: Instructions for using open-weight models (e.g., via Ollama or LM Studio) as a substitute when neither subscription is available
- **Language-specific guides**: Dedicated pages for Stata, R, Python, and MATLAB workflows with Claude
- **Advanced topics**: Custom MCP servers, CI/CD integration, automated testing pipelines
- **Data security**: Guidelines for working with sensitive or restricted-use data alongside AI tools
