# RA Manual

A practical guide for research assistants on using AI tools to accelerate research workflows.

---

## The 6 Principles

These are the habits that separate productive AI-assisted coding from frustrating trial-and-error. Internalize these and you'll 10x your output.

### 1. Always Plan First

Never let the AI start coding immediately. Use **plan mode** to have it research the codebase, identify the right approach, and write out a step-by-step plan for your approval. Planning prevents wasted work and ensures alignment before a single line of code is written.

### 2. Use Compound Engineering

Break complex tasks into smaller, well-defined pieces. Let the AI complete one step, verify it works, then move to the next. This creates reliable, reviewable progress instead of a giant diff you can't understand.

### 3. Use Sub-Agents Liberally

Spawn specialized sub-agents for research, exploration, and parallel tasks. Don't try to do everything in one conversation thread. Sub-agents can search codebases, read documentation, and gather context while you focus on the main task.

### 4. Create Skills for Repetitive Tasks

When you find yourself repeating the same instructions, create a **skill** (a reusable prompt template). Skills turn multi-step workflows into one-command operations. Build your personal library of skills over time.

### 5. Keep Up with Best Practices

AI coding tools evolve rapidly. Read the official documentation regularly. What was best practice last month may be outdated. Stay current with:

- [Anthropic's Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Claude Code Best Practices](https://docs.anthropic.com/en/docs/claude-code/best-practices)
- [Anthropic's Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)

### 6. Use Voice-to-Text

You can speak at ~150 words per minute but only type ~50. Use voice-to-text software like [Wispr Flow](https://www.wispr.ai/) to dictate your prompts, explanations, and code comments. This alone can 3x your input speed and reduces the friction of communicating with AI.

---

## What This Manual Covers

This manual teaches you how to work effectively with AI coding assistants. We use **Claude Code in VS Code** as our primary example, but the principles apply broadly — whether you're using ChatGPT, Cursor, Copilot, or other tools.

AI is a force multiplier for research. Used well, it dramatically speeds up data cleaning, code writing, debugging, and even helps implement economic models from paper descriptions. Used poorly, it produces plausible-looking garbage. This manual shows you how to use it well.

## Pages

1. **[Setup](01-setup.md)** — Install VS Code and Claude Code
2. **[Why AI Coding Tools?](02-why-claude-code.md)** — What makes these tools useful for research, with concrete examples
3. **[Core Workflow](03-workflow.md)** — Plan mode, sub-agents, compound engineering in practice
4. **[Code Principles](04-code-principles.md)** — Project organization and coding standards
5. **[Resources](05-resources.md)** — Links to documentation and further reading

## Quick Start

1. Follow [Setup](01-setup.md) to install everything
2. Read the **6 Principles** above — this is the most important part
3. Work through [Core Workflow](03-workflow.md) to see the principles in action
4. Keep [Code Principles](04-code-principles.md) bookmarked as a reference
