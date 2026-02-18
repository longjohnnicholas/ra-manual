# Getting the Most from Coding with Agents

These tools and practices work across AI coding agents — Claude Code, Open Code, Cursor, GitHub Copilot, and others. The concepts are the same; only the file paths and keybindings differ.

---

**On this page:**

- [Project Context Files](#project-context-files) — AGENTS.md and CLAUDE.md
- [Skills](#skills) — reusable instructions for repeated tasks
- [Plan Mode](#plan-mode) — always plan before coding
- [Sub-Agents](#sub-agents) — parallel work and code review
- [Compound Engineering](#compound-engineering) — learning from every session
- [The Compound Engineering Plugin](#the-compound-engineering-plugin) — pre-built agents and workflows
- [Working with PDFs](#working-with-pdfs) — minimize token usage
- [Working with LaTeX and Overleaf](#working-with-latex-and-overleaf) — use agents with Overleaf

---

## Project Context Files

### What they are

A project context file is a markdown file that your AI agent reads automatically at the start of every conversation. It gives the agent context it can't infer from code alone — project goals, conventions, common pitfalls, and how to run things.

There are two conventions:

- **`AGENTS.md`** — the open standard, supported by 20+ tools (Open Code, Cursor, Copilot, Codex, Gemini CLI, and more). Governed by the [Agentic AI Foundation](https://aaif.io/) under the Linux Foundation.
- **`CLAUDE.md`** — Claude Code's equivalent. Same concept, different filename.

### Which file should you use?

| Tool | Reads | Also reads |
|------|-------|------------|
| **Open Code** | `AGENTS.md` | `CLAUDE.md` (fallback) |
| **Claude Code** | `CLAUDE.md` | — |
| **Cursor** | `AGENTS.md` | `.cursor/rules/` |
| **GitHub Copilot** | `AGENTS.md` | `.github/copilot-instructions.md` |
| **OpenAI Codex** | `AGENTS.md` | — |

!!! tip "Cross-tool compatibility"
    If you use multiple tools (or might switch later), create an `AGENTS.md` as your primary file. Then make Claude Code read it too with a one-line `CLAUDE.md`:

    ```markdown
    @AGENTS.md
    ```

    Or create a symlink: `ln -s AGENTS.md CLAUDE.md`

    This way, you maintain one file that works everywhere.

### Why you need one

Without a project context file, you'd have to re-explain your project every session. With one, the agent starts every conversation already knowing:

- What the project is about
- Your coding conventions
- Known gotchas and edge cases
- How to run scripts and tests

This saves time and prevents repeated mistakes.

### Where to save it

=== "Open Code"

    | Location | Scope |
    |----------|-------|
    | `./AGENTS.md` | This project |
    | `./code/AGENTS.md` | This task subfolder |
    | `~/.config/opencode/AGENTS.md` | All your projects |

=== "Claude Code"

    | Location | Scope | Git? |
    |----------|-------|------|
    | `./CLAUDE.md` | This project | Yes |
    | `./code/CLAUDE.md` | This task subfolder | Yes |
    | `~/.claude/CLAUDE.md` | All your projects | No |
    | `./CLAUDE.local.md` | Personal overrides | No (gitignore it) |

Both tools read these recursively — if you're working in `cleaning/survey_data/code/`, the agent picks up context files from that directory and all parent directories.

### Best practices

**Keep it short.** Only include things the agent would get wrong without. For each line, ask: *"Would removing this cause a mistake?"* If not, cut it.

**Update it at the end of each session.** Ask: *"Is there anything we learned that should go into AGENTS.md?"* Add useful learnings. This is how knowledge compounds.

**Example:**

```markdown
# Project context
Estimates effect of trade liberalization on firm productivity
using Indonesian manufacturing census (1991-2000).

# Conventions
- Stata for cleaning/regressions, Python for figures
- Relative paths only
- Script naming: 01_, 02_, etc.

# Commands
- Run all: `stata -b do code/run_all.do`

# Gotchas
- Raw data has duplicate firm IDs in 1995 — deduplicate first
- Variable `lnrev` is log revenue, NOT level
```

!!! tip
    Run `/init` to auto-generate a starter context file for your project. Both Claude Code and Open Code support this command.

---

## Skills

### What they are

Skills are markdown files containing specialist instructions for tasks you do repeatedly. Instead of re-typing the same prompt every time, you create a skill once and invoke it with a slash command.

Think of them as saved prompts with superpowers — they can include detailed instructions, checklists, and even specify which tools the agent should use.

The skill format (`SKILL.md` with YAML frontmatter) is an [open standard](https://agentskills.io/specification) that works across Claude Code, Open Code, GitHub Copilot, Cursor, and others.

### Why they're useful

- **Save time** — don't re-explain the same task every session
- **Consistency** — the task is done the same way every time
- **Shareable** — your team can use the same skills
- **Composable** — combine multiple skills for complex workflows
- **Portable** — the same SKILL.md works in different tools

### Where to save them

=== "Open Code"

    | Location | Scope |
    |----------|-------|
    | `.opencode/skills/<skill-name>/SKILL.md` | This project |
    | `.agents/skills/<skill-name>/SKILL.md` | This project (alt) |
    | `.claude/skills/<skill-name>/SKILL.md` | This project (Claude Code compat) |
    | `~/.config/opencode/skills/<skill-name>/SKILL.md` | All projects |

    Open Code searches all these paths, so skills written for Claude Code work automatically.

=== "Claude Code"

    | Location | Scope |
    |----------|-------|
    | `.claude/skills/<skill-name>/SKILL.md` | This project |
    | `~/.claude/skills/<skill-name>/SKILL.md` | All projects |

### Example: Running regressions

```markdown
# .claude/skills/run-regressions/SKILL.md
---
name: run-regressions
description: Run the main regression specifications
---

When asked to run regressions:
1. Check that cleaned data exists in output/cleaned/
2. Run code/analysis/01_main_regressions.do
3. Verify output/tables/ contains the expected .tex files
4. Report any errors from the Stata log
```

Invoke with `/run-regressions` or just describe what you want — the agent auto-detects relevant skills.

### Example: Weekly task update

```markdown
# .claude/skills/weekly-update/SKILL.md
---
name: weekly-update
description: Update the weekly task list for supervisor meeting
---

Update my weekly task markdown file:
1. Move "Next Week" items to "This Week"
2. Add links to any Trello cards or Google Drive files I mention
3. Ask me what I plan to do next week
4. Format as a clean 2-column table
```

---

## Plan Mode

**Never let the agent start coding immediately on a complex task.** Always start in plan mode.

### What it does

The agent analyzes your codebase with read-only access. It can read files, search code, and explore — but won't edit anything until you approve.

### How to activate it

=== "Claude Code"

    - Keyboard: `Shift+Tab` twice (you'll see "plan mode on")
    - Command: `/plan`
    - CLI: `claude --permission-mode plan`

=== "Open Code"

    - Press **Tab** to switch to the **plan** agent (read-only analysis)
    - Press **Tab** again to switch back to the **build** agent (full access)

    Open Code has two built-in agents: `plan` (read-only) and `build` (full access). Switching between them is how you control what the agent can do.

### The workflow

1. **Explain** what you want. Be specific about the goal, not the implementation.
2. **Ask for a plan.** Say: *"Create a detailed plan. Break it into steps."*
3. **Review and iterate.** Push back, ask questions. This is where 80% of the value is.
4. **Ask about parallelization.** *"Can any of these steps run in parallel with sub-agents?"*
5. **Approve and execute.** Switch to build/normal mode to let the agent work.
6. **Review the output** before committing.

!!! warning
    Skipping plan mode is the #1 cause of agents producing unusable code.

---

## Sub-Agents

Sub-agents are separate AI instances that handle specific subtasks. Use them for parallelization and code review.

### Parallelization

When your plan has independent steps, run them in parallel:

```
These three tasks are independent — clean the trade data, clean the firm
data, and clean the tariff data. Use sub-agents to do all three in parallel.
```

Each sub-agent works in its own context and returns results to the main conversation.

### Code review

After the agent finishes a task, launch a review sub-agent:

```
Launch a sub-agent to review the code you just wrote. Check for:
- Correctness of the implementation
- Edge cases and error handling
- Whether it follows our AGENTS.md conventions
```

This catches mistakes the "author" agent might miss — like a second pair of eyes on a PR.

### Custom sub-agents

For repeated review tasks, create custom agents:

=== "Open Code"

    Save in `.opencode/agents/` or `~/.config/opencode/agents/`:

    ```markdown
    # .opencode/agents/code-reviewer.md
    ---
    name: code-reviewer
    description: Reviews code for correctness and conventions
    tools: Read, Grep, Glob
    ---

    You are a code reviewer for an economics research project.
    Check for:
    - Logical correctness (do regressions match the spec?)
    - Data handling (are merges correct? dropped observations?)
    - Style (follows AGENTS.md conventions?)
    - Reproducibility (relative paths? seeds set?)

    Be specific. Reference line numbers. Suggest fixes.
    ```

=== "Claude Code"

    Save in `.claude/agents/`:

    ```markdown
    # .claude/agents/code-reviewer.md
    ---
    name: code-reviewer
    description: Reviews code for correctness and conventions
    tools: Read, Grep, Glob
    model: sonnet
    ---

    You are a code reviewer for an economics research project.
    Check for:
    - Logical correctness (do regressions match the spec?)
    - Data handling (are merges correct? dropped observations?)
    - Style (follows CLAUDE.md conventions?)
    - Reproducibility (relative paths? seeds set?)

    Be specific. Reference line numbers. Suggest fixes.
    ```

---

## Compound Engineering

The practice that makes you better over time. **Every session should make the next session easier.**

### The loop

1. **Plan** — create a step-by-step plan with the agent
2. **Work** — let the agent execute the plan
3. **Assess** — use a sub-agent to review the work
4. **Compound** — ask what should go into AGENTS.md or a skill

### The key habit

After every task, ask:

```
Is there anything we learned from this session that should go into
AGENTS.md so we don't make the same mistakes again?
```

The agent might say: *"The merge on firm_id needs to be many-to-one because of the panel structure. We should note that."* Add it to your context file. Future sessions start with that knowledge.

### Why it matters

Over weeks and months, your context file becomes an institutional knowledge base. New RAs inherit all the lessons learned. The agent stops making the same mistakes. The whole team gets faster.

This is what separates productive AI-assisted coding from frustrating trial-and-error.

---

## The Compound Engineering Plugin

The compound engineering loop above is powerful on its own, but [Every, Inc.](https://every.to) has built an open-source plugin that gives you **pre-built agents, skills, and workflows** that automate the entire cycle. Instead of manually asking the agent to plan, review, and document learnings, you get slash commands that do it for you with specialized sub-agents running in parallel.

**What you get:**

| Category | What's included |
|---|---|
| **Workflow commands** | `/workflows:plan`, `/workflows:work`, `/workflows:review`, `/workflows:compound`, `/workflows:brainstorm` |
| **Review agents (15)** | Security analysis, performance profiling, architecture review, Rails/Python/TypeScript reviewers, database migration checks, and more |
| **Research agents (5)** | Framework docs lookup, git history analysis, best practices research, codebase exploration |
| **Design agents (3)** | Figma-to-code comparison, iterative design refinement |
| **Context7 MCP** | Real-time documentation lookup for 100+ frameworks |

### The core workflow

The plugin turns the compound engineering loop into four slash commands:

1. **`/workflows:brainstorm`** — Clarify fuzzy requirements through guided questioning before you start
2. **`/workflows:plan`** — Convert a feature idea into a detailed implementation plan. Sub-agents research your codebase and external best practices in parallel
3. **`/workflows:work`** — Execute the plan with task tracking
4. **`/workflows:review`** — Deploy 15+ specialized review agents simultaneously (security, performance, architecture, code style, etc.)
5. **`/workflows:compound`** — Document what you learned so the next session starts smarter

The philosophy is roughly **80% planning and review, 20% execution.** The plugin enforces this by making the planning and review steps as easy as typing a slash command.

### Installing in Claude Code

Run these two commands inside a Claude Code session:

```bash
# Add the plugin marketplace
/plugin marketplace add https://github.com/EveryInc/compound-engineering-plugin

# Install the plugin
/plugin install compound-engineering
```

That's it. You'll immediately have access to all the slash commands and agents.

### Installing in Open Code

Use the cross-platform installer:

```bash
bunx @every-env/compound-plugin install compound-engineering --to opencode
```

This writes the plugin configuration to `~/.config/opencode/`. All agents, skills, and commands will be available the next time you launch Open Code.

Alternatively, add it manually in your `opencode.json`:

```json
{
  "plugin": ["@every-env/compound-plugin"]
}
```

### What the review agents actually do

When you run `/workflows:review`, the plugin launches multiple specialized sub-agents **in parallel** to review your code from different angles:

- **Security sentinel** — checks for vulnerabilities, input validation, auth issues
- **Performance oracle** — analyzes algorithmic complexity, database queries, memory usage
- **Architecture strategist** — evaluates whether changes follow established patterns
- **Code simplicity reviewer** — flags over-engineering and unnecessary complexity
- **Data integrity guardian** — reviews migrations, data constraints, transaction safety
- **Language-specific reviewers** — Python, TypeScript, and Rails reviewers with idiomatic style checks

Each agent returns specific findings with line numbers and suggested fixes. It's like having six experienced developers review your PR simultaneously.

### Recommended project structure

The plugin works best when your project follows this layout:

```
project/
├── AGENTS.md              # Agent instructions and patterns
├── docs/
│   ├── brainstorms/       # Output from /workflows:brainstorm
│   ├── plans/             # Output from /workflows:plan
│   └── solutions/         # Documented problems and solutions
└── todos/                 # Prioritized work items
```

The `/workflows:compound` command automatically updates your context file and creates entries in `docs/solutions/` so learnings are searchable across future sessions.

!!! tip "Start here"
    After installing, try running `/workflows:plan` on your next task instead of jumping straight into coding. The difference in output quality is significant.

:material-github: **[EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin)** — full source, documentation, and changelog.

---

## Working with PDFs

**PDFs are expensive.** Uploading a PDF consumes a large number of tokens because the agent must process the entire document as an image. A 20-page paper can easily use 50,000+ tokens — enough context for an entire coding session.

### Best practices

1. **Convert to text first.** Extract text from PDFs before uploading. A `.txt` file is far cheaper to read than a PDF.

    ```bash
    # Using pdftotext (install with: brew install poppler)
    pdftotext paper.pdf paper.txt
    ```

2. **Use sub-agents to find relevant sections.** Instead of loading a full document, ask a sub-agent to search for specific content:

    ```
    Launch a sub-agent to search paper.txt for the section on
    identification strategy. Return only that section.
    ```

3. **Split large documents.** Break lengthy PDFs into chapters or sections. Only load the parts you actually need for the current task.

4. **Summarize first.** If you need the gist of a long document, ask the agent to summarize the text file before diving into details.

!!! warning
    Never upload a PDF "just in case" you might need it. Each upload burns through your context budget.

---

## Working with LaTeX and Overleaf

Overleaf is great for collaborative LaTeX editing, but its interface doesn't support AI coding agents. Here's how to get the best of both worlds.

### The workflow

1. **Clone from Overleaf.** Use Overleaf's Git integration to clone your project locally:

    ```bash
    git clone https://git.overleaf.com/your-project-id my-paper
    cd my-paper
    ```

    (Find your Git URL in Overleaf: Menu → Git)

2. **Edit with your agent.** Open the folder in VS Code or the Open Code desktop app. Now you have full access to skills, sub-agents, and all the features covered in this guide.

3. **Push back to Overleaf.** When done, commit and push:

    ```bash
    git add . && git commit -m "Revised introduction" && git push
    ```

    Your changes appear instantly in Overleaf.

### Avoiding conflicts

If multiple co-authors are working simultaneously:

- **Pull before you start.** Always `git pull` before editing.
- **Communicate.** Let co-authors know when you're doing a heavy editing session.
- **Commit frequently.** Small commits merge more easily than large ones.

### Why not the Chrome extension?

Claude's browser extension can help with writing, but it can't run specialized skills, use sub-agents, or read your project context file. For serious paper drafting, the local Git workflow is worth the setup.
