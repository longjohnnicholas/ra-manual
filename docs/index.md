---
hide:
  - navigation
  - toc
---

# RA Manual

A practical guide for research assistants on using AI tools.

---

## Key Principles

These are the habits that matter. Read them, internalize them, come back to them.

1. **Always plan first.** Never let AI start coding immediately. Use plan mode to research the codebase, identify the right approach, and write a step-by-step plan for your approval. Planning prevents wasted work.

2. **Mind your model usage.** Default to Sonnet for most tasks—you'll burn through credits fast with Opus. Save Opus for complex reasoning only.

3. **Work in markdown.** Markdown files are easy for AI to read, edit, and search. Use them for notes, documentation, task lists, and meeting agendas. AI works better with markdown than Word docs or PDFs.

4. **Keep a weekly task list.** Maintain a markdown file with a simple table: *This Week* (what you did, with links to Trello cards or Google Drive files) and *Next Week* (what you're planning). Share it with your supervisor before each meeting. AI can help you update it.

5. **Use compound engineering.** The loop is: *Plan → Work → Assess → Compound*. Break tasks into small pieces, let AI execute step-by-step, then review the results. The crucial step is **compounding**: after each task, ask "what could we have done better?" and write those learnings into your `CLAUDE.md` file or skill. This way the AI learns from past mistakes and gets smarter over time.

6. **Use sub-agents liberally.** Spawn specialized sub-agents for research, exploration, and parallel tasks. Don't try to do everything in one conversation thread.

7. **Create skills for repetitive tasks.** When you find yourself repeating the same instructions, create a skill (a reusable prompt template). Build your personal library over time.

8. **Keep up with best practices.** AI tools evolve rapidly. Read the [official docs](https://docs.anthropic.com/en/docs/claude-code) regularly. Last month's best practice may be outdated.

9. **Use voice-to-text.** You can speak at ~150 wpm but only type ~50 wpm. Use [Wispr Flow](https://www.wispr.ai/) to 3x your input speed.

---

## Get Started

<div class="grid cards" markdown>

-   :material-download:{ .lg .middle } __Setup__

    ---

    Install VS Code and Claude Code.

    [:octicons-arrow-right-24: Installation guide](01-setup.md)

-   :material-lightbulb-on-outline:{ .lg .middle } __Why AI Coding Tools?__

    ---

    What makes these tools useful for research.

    [:octicons-arrow-right-24: Learn more](02-why-claude-code.md)

-   :material-rocket-launch-outline:{ .lg .middle } __Core Workflow__

    ---

    Plan mode, sub-agents, compound engineering.

    [:octicons-arrow-right-24: See the workflow](03-workflow.md)

-   :material-link-variant:{ .lg .middle } __Resources__

    ---

    Documentation, tutorials, and tools.

    [:octicons-arrow-right-24: Browse resources](05-resources.md)

</div>
