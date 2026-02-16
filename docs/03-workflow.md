# Core Workflow

This section covers the practices that separate effective Claude Code usage from mediocre usage. Follow these and you'll get dramatically better results.

## The CLAUDE.md File

A `CLAUDE.md` file is a special markdown file that Claude reads automatically at the start of every conversation. It gives Claude persistent context it can't infer from your code alone.

**Where to save it:**

- **Project root** (`./CLAUDE.md`): Applies to this project. Check it into git so your whole team benefits.
- **Home directory** (`~/.claude/CLAUDE.md`): Applies to all your projects across every session.
- **Local override** (`./CLAUDE.local.md`): Personal project settings. Add this to `.gitignore`.

Claude reads these recursively — if you're working in `code/analysis/`, it picks up `CLAUDE.md` files from that directory, `code/`, and the project root.

**What to put in it:**

```markdown
# Project context
This project estimates the effect of trade liberalization on firm productivity
using Indonesian manufacturing census data (1991-2000).

# Code conventions
- Use Stata for data cleaning and regressions
- Use Python for simulations and figures
- All paths should be relative to the project root
- Use `01_`, `02_` prefixes for script ordering

# Common commands
- Run all analysis: `stata -b do code/run_all.do`
- Build figures: `python code/figures/make_all.py`

# Gotchas
- The raw data has duplicate firm IDs in 1995 — always deduplicate first
- Variable `lnrev` is log revenue, NOT level revenue
```

**What NOT to put in it:** anything Claude can figure out by reading your code. Keep it concise. For each line, ask: *"Would removing this cause Claude to make a mistake?"* If not, cut it.

!!! tip
    Run `/init` in Claude Code to auto-generate a starter `CLAUDE.md` based on your project.

## Skills

Skills are reusable instruction sets for specific tasks. Think of them as recipes Claude can follow.

**Where they live:** `.claude/skills/<skill-name>/SKILL.md` (project-level) or `~/.claude/skills/<skill-name>/SKILL.md` (global).

**Example:** A skill for running regressions in your project:

```markdown
# .claude/skills/run-regressions/SKILL.md
---
name: run-regressions
description: Run the main regression specifications for this project
---

When asked to run regressions:
1. Check that cleaned data exists in output/cleaned/
2. Run code/analysis/01_main_regressions.do
3. Verify that output/tables/ contains the expected .tex files
4. Report any errors or warnings from the Stata log
```

Invoke a skill by typing `/run-regressions` or just describe what you want and Claude will auto-detect the relevant skill.

## Think Out Loud

A useful mental model: treat Claude Code like a conversation, not a command line. Rather than giving it a fully-specified instruction, think out loud. Describe what you're trying to do, what you're unsure about, what the data looks like. Claude will propose an approach, you steer it, and the dialogue becomes the thinking process.

This is especially powerful for research tasks where you don't know the exact implementation upfront — you know the economic question, and Claude helps you figure out how to answer it in code.

## Always Start in Plan Mode

This is the single most important workflow habit. **Never let Claude start coding immediately on a complex task.** Instead, start in plan mode.

**What plan mode does:** Claude analyzes your codebase with read-only access. It can read files, search code, and explore the directory — but it won't edit anything or run commands until you approve.

**How to activate it:**

- Keyboard: press `Shift+Tab` twice (you'll see "plan mode on")
- Command: type `/plan`
- CLI flag: `claude --permission-mode plan`

![Plan mode indicator in Claude Code](images/plan-mode.png)

**The workflow:**

1. **Explain** what you want in natural language. Be specific about the goal, not the implementation.
2. **Ask Claude to make a plan.** Say: *"Create a detailed plan for how you'd implement this. Break it into steps."*
3. **Review the plan.** Push back, ask questions, iterate. This is where 80% of the value is.
4. **Ask Claude to parallelize.** Say: *"Which of these steps can be done in parallel using sub-agents?"*
5. **Approve and switch to normal mode** (`Shift+Tab`) to let Claude execute.
6. **Review the output** before committing.

!!! warning
    Skipping plan mode on complex tasks is the #1 cause of Claude producing unusable code. Take the extra 2 minutes to plan.

## Sub-Agents: Review and Parallelization

Sub-agents are separate Claude instances that handle specific subtasks. They're powerful for two things.

### Parallelization

When your plan has independent steps, ask Claude to run them in parallel:

```
These three tasks are independent — clean the trade data, clean the firm data,
and clean the tariff data. Use sub-agents to do all three in parallel.
```

Each sub-agent works in its own context and returns results to the main conversation. This is dramatically faster than doing things sequentially.

When planning, always ask: *"Can any of these steps be parallelized?"*

### Code Review

After Claude finishes a task, launch a sub-agent to review the work:

```
Launch a sub-agent to review the code you just wrote. Check for:
- Correctness of the implementation
- Edge cases and error handling
- Whether it follows our project conventions in CLAUDE.md
```

This catches mistakes that the "author" Claude might miss — just like having a second pair of eyes on a pull request.

### Custom Sub-Agents

For tasks you do repeatedly, create custom agents in `.claude/agents/`:

```markdown
# .claude/agents/code-reviewer.md
---
name: code-reviewer
description: Reviews code for correctness, style, and project conventions
tools: Read, Grep, Glob
model: sonnet
---

You are a careful code reviewer for an economics research project.
Review the specified code for:
- Logical correctness (do the regressions match the specification?)
- Data handling (are merges correct? any dropped observations?)
- Style (does it follow the project's CLAUDE.md conventions?)
- Reproducibility (are paths relative? are seeds set?)

Be specific. Reference line numbers. Suggest fixes.
```

## Compound Engineering

This is the practice that makes you better over time. The idea is simple: **every session should make the next session easier.**

After Claude finishes a task, always end with this question:

```
Is there anything we learned from this session that should go into the
CLAUDE.md file so we don't make the same mistakes again?
```

Claude might say: *"Yes — the merge on firm_id needs to be a many-to-one merge because of the panel structure. We should note that."* You add it to `CLAUDE.md`, and every future session starts with that knowledge.

**The compound loop:**

1. **Plan** — understand the task, create a plan with Claude
2. **Execute** — let Claude implement the plan
3. **Review** — use a sub-agent to check the work
4. **Compound** — ask what should go into `CLAUDE.md`

Over weeks and months, your `CLAUDE.md` file becomes an institutional knowledge base. New RAs who join the project inherit all the lessons learned. Claude stops making the same mistakes. The whole team gets faster.

!!! tip
    You can also install the **Compound Engineering plugin** from the Claude Code marketplace to automate parts of this loop. Or just do it manually — the habit matters more than the tooling.
