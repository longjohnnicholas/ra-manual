# Getting the Most from Claude Code

This page covers the tools and practices that make Claude Code powerful: CLAUDE.md files, skills, sub-agents, and the compound engineering workflow.

---

**On this page:**

- [CLAUDE.md Files](#claudemd-files) — persistent project context
- [Skills](#skills) — reusable instructions for repeated tasks
- [Plan Mode](#plan-mode) — always plan before coding
- [Sub-Agents](#sub-agents) — parallel work and code review
- [Compound Engineering](#compound-engineering) — learning from every session

---

## CLAUDE.md Files

### What it is

A `CLAUDE.md` file is a markdown file that Claude reads automatically at the start of every conversation. It gives Claude context about your project that it can't infer from code alone—things like project goals, conventions, common pitfalls, and how to run things.

### Why you need one

Without a `CLAUDE.md`, you'd have to re-explain your project context every session. With one, Claude starts every conversation already knowing:

- What the project is about
- Your coding conventions
- Known gotchas and edge cases
- How to run scripts and tests

This saves time and prevents repeated mistakes.

### Where to save it

| Location | Scope | Git? |
|----------|-------|------|
| `./code/CLAUDE.md` | This task subfolder | Yes |
| `./CLAUDE.md` | Whole project | Yes |
| `~/.claude/CLAUDE.md` | All your projects | No |
| `./CLAUDE.local.md` | Personal overrides | No (gitignore it) |

Claude reads these recursively—if you're working in `cleaning/survey_data/code/`, it picks up CLAUDE.md files from that directory and all parent directories.

### Best practices

**Keep it short.** Only include things Claude would get wrong without. For each line, ask: *"Would removing this cause Claude to make a mistake?"* If not, cut it.

**Update it at the end of each session.** Ask Claude: *"Is there anything we learned that should go into CLAUDE.md?"* Add useful learnings. This is how knowledge compounds.

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
    Run `/init` to auto-generate a starter CLAUDE.md for your project.

---

## Skills

### What they are

Skills are markdown files containing specialist instructions for tasks you do repeatedly. Instead of re-typing the same prompt every time, you create a skill once and invoke it with a slash command.

Think of them as saved prompts with superpowers—they can include detailed instructions, checklists, and even specify which tools Claude should use.

### Why they're useful

- **Save time** — don't re-explain the same task every session
- **Consistency** — the task is done the same way every time
- **Shareable** — your team can use the same skills
- **Composable** — combine multiple skills for complex workflows

### Where to save them

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

Invoke with `/run-regressions` or just describe what you want—Claude auto-detects relevant skills.

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

**Never let Claude start coding immediately on a complex task.** Always start in plan mode.

### What it does

Claude analyzes your codebase with read-only access. It can read files, search code, and explore—but won't edit anything until you approve.

### How to activate it

- Keyboard: `Shift+Tab` twice (you'll see "plan mode on")
- Command: `/plan`
- CLI: `claude --permission-mode plan`

### The workflow

1. **Explain** what you want. Be specific about the goal, not the implementation.
2. **Ask for a plan.** Say: *"Create a detailed plan. Break it into steps."*
3. **Review and iterate.** Push back, ask questions. This is where 80% of the value is.
4. **Ask about parallelization.** *"Can any of these steps run in parallel with sub-agents?"*
5. **Approve and execute.** Switch to normal mode (`Shift+Tab`) to let Claude work.
6. **Review the output** before committing.

!!! warning
    Skipping plan mode is the #1 cause of Claude producing unusable code.

---

## Sub-Agents

Sub-agents are separate Claude instances that handle specific subtasks. Use them for parallelization and code review.

### Parallelization

When your plan has independent steps, run them in parallel:

```
These three tasks are independent — clean the trade data, clean the firm
data, and clean the tariff data. Use sub-agents to do all three in parallel.
```

Each sub-agent works in its own context and returns results to the main conversation.

### Code review

After Claude finishes a task, launch a review sub-agent:

```
Launch a sub-agent to review the code you just wrote. Check for:
- Correctness of the implementation
- Edge cases and error handling
- Whether it follows our CLAUDE.md conventions
```

This catches mistakes the "author" Claude might miss—like a second pair of eyes on a PR.

### Custom sub-agents

For repeated review tasks, create custom agents in `.claude/agents/`:

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

1. **Plan** — create a step-by-step plan with Claude
2. **Work** — let Claude execute the plan
3. **Assess** — use a sub-agent to review the work
4. **Compound** — ask what should go into CLAUDE.md or a skill

### The key habit

After every task, ask:

```
Is there anything we learned from this session that should go into
CLAUDE.md so we don't make the same mistakes again?
```

Claude might say: *"The merge on firm_id needs to be many-to-one because of the panel structure. We should note that."* Add it to CLAUDE.md. Future sessions start with that knowledge.

### Why it matters

Over weeks and months, your CLAUDE.md becomes an institutional knowledge base. New RAs inherit all the lessons learned. Claude stops making the same mistakes. The whole team gets faster.

This is what separates productive AI-assisted coding from frustrating trial-and-error.
