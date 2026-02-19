---
title: "Refactor setup page to Claude Code and Codex CLI"
type: refactor
status: completed
date: 2026-02-18
---

# Refactor Setup Page: Claude Code and Codex CLI

## Overview

Replace the current three-option setup page (Claude Code, Open Code + OpenRouter, Open Code Desktop) with a simpler two-path structure: **VS Code first, then pick your AI agent** (Claude Code or Codex CLI). Drop Open Code and OpenRouter entirely.

## Problem Statement / Motivation

The current setup page offers OpenRouter as a second path, which requires a shared API key, cost management, and model selection decisions — complexity that distracts from the real goal: getting RAs coding with an AI agent. Both Claude Code and Codex CLI now offer equivalent features at $20/mo subscription tiers, making the OpenRouter workaround unnecessary.

## Proposed Solution

### New Page Structure

```
Setup
├── Intro (pick one of two options, ~10 min setup)
├── Step 1: Install VS Code (same for everyone)
├── Step 2: Pick your AI agent
│   ├── Option A: Claude Code (Claude Pro/Max/Team)
│   │   ├── Install CLI (tabs: Mac curl / Mac brew / Windows PS)
│   │   ├── Install VS Code extension
│   │   ├── Authenticate
│   │   └── Brief note: sidebar panel + terminal modes
│   └── Option B: Codex CLI (ChatGPT Plus/Pro)
│       ├── Install CLI (tabs: Mac brew / npm / Windows note)
│       ├── Install VS Code extension
│       ├── Authenticate
│       └── Brief note: sidebar panel + terminal modes
├── Which should I pick? (decision guide)
└── Verify Installation
```

### Key Design Decisions

1. **VS Code is mandatory** — it's the workbench that hosts both AI agents plus Stata extensions for the "select and run" workflow RAs need
2. **No pricing tables** — just state the subscription requirement and move on
3. **Symmetric structure** — both options follow the same 3-step pattern (CLI → extension → auth) so the page is easy to scan
4. **Brief usage modes** — one sentence noting sidebar panel + terminal exist, not dedicated cards
5. **Decision guide** — a small callout helping RAs who have no preference ("Already have Claude? Pick A. Already have ChatGPT? Pick B. Neither? Ask your advisor.")

## Files to Modify

### Primary: `docs/01-setup.md`

Complete rewrite. New content:

**Intro section** — Two grid cards at top (Claude Code, Codex CLI) with jump links, matching existing pattern.

**Step 1: Install VS Code** — Identical to current page. Keep the download link and "launch once to verify" instruction.

**Option A: Claude Code** — Keep current content with minor edits:
- Install CLI (3 OS tabs: Mac/Linux curl, Windows PowerShell, Homebrew)
- Install VS Code extension (`Cmd+Shift+X` → search "Claude Code")
- Authenticate (`claude` in terminal → browser sign-in)
- One-liner: "Use Claude from the sidebar panel (click the icon) or the terminal (`claude`)"

**Option B: Codex CLI** — New section, parallel structure:
- Install CLI (3 tabs: Homebrew Mac, npm, Windows note)
  - Homebrew tab: `brew install --cask codex`
  - npm tab: `npm i -g @openai/codex` with note that Node.js is required (link to nodejs.org)
  - Windows tab: note that npm path works in PowerShell if Node.js is installed; link to Node.js installer
- Install VS Code extension (`Cmd+Shift+X` → search "ChatGPT" by OpenAI)
- Authenticate (`codex` in terminal → browser sign-in)
- One-liner: "Use Codex from the sidebar panel or the terminal (`codex`)"

**Which should I pick?** — Admonition (`!!! tip`):
- "Already have a Claude subscription? → Option A"
- "Already have a ChatGPT subscription? → Option B"
- "Neither? Ask your advisor which the team uses."
- "Both work equally well for research tasks."

**Verify Installation** — Keep existing section, make tool-agnostic. The prompt "What files are in this directory?" works for both tools.

**Migration note** — Small `!!! info` callout at top of page: "Previously using Open Code or OpenRouter? Either option below is a direct replacement."

### Secondary: `docs/index.md`

- **Line 83:** Change "Three options: Claude Code, Open Code + OpenRouter, or the Open Code desktop app." → "Two options: Claude Code (Anthropic) or Codex CLI (OpenAI)."
- **Line 99:** Change "works across Claude Code, Open Code, and more" → "works across Claude Code, Codex CLI, and other AI coding agents"

### Tertiary: Other pages to audit

- `docs/03-workflow.md` — Check for Open Code / OpenRouter references in tabs. Update tabs from `=== "Open Code"` to `=== "Codex CLI"` with corresponding content.
- `docs/05-resources.md` — Check for OpenRouter links or references.
- `docs/06-connected-tools.md` — Check for tool-specific references.
- `README.md` — Line 33 references "VS Code + Claude Code installation" — update to reflect both options.

## Edge Cases to Address

From SpecFlow analysis:

1. **Node.js prerequisite for Codex npm install** — Add explicit note + link to nodejs.org LTS. Recommend Homebrew as primary Mac path to avoid this.
2. **Windows users and Codex** — npm works if Node is installed. Document this explicitly. Claude Code has a cleaner Windows path (PowerShell one-liner).
3. **Subscription tier clarity** — ChatGPT Plus ($20/mo) includes Codex CLI with usage limits. Pro ($200/mo) has higher limits. State "ChatGPT Plus or Pro" and note that Plus is sufficient for most RA work.
4. **Team-provided subscriptions** — Add a callout: "If your advisor is providing the subscription, ask them to add your email to the team workspace before you begin."
5. **Both tools can coexist** — Brief note that installing both is fine if someone wants to try both.

## What to Remove

- Entire "Option 2: Open Code + OpenRouter" section (~180 lines)
- OpenRouter API key instructions
- Model cost comparison table
- Model switching by task complexity table
- Open Code Desktop App section
- All OpenRouter references site-wide

## Acceptance Criteria

- [x] Setup page has exactly two paths: Claude Code and Codex CLI
- [x] Both paths follow identical structure (CLI → extension → auth)
- [x] No references to Open Code or OpenRouter remain anywhere in docs/
- [x] VS Code install step appears before both options (shared step)
- [x] Decision guide helps users who have no preference
- [x] Windows path is documented for both tools
- [x] Node.js prerequisite is noted for Codex npm install
- [x] Verify step works for both tools
- [x] `index.md` updated to reflect two options
- [x] Page renders correctly with `mkdocs serve`

## References

### Research Sources
- [Codex CLI official docs](https://developers.openai.com/codex/cli/)
- [Codex VS Code extension](https://marketplace.visualstudio.com/items?itemName=openai.chatgpt)
- [Codex pricing](https://developers.openai.com/codex/pricing/)
- [Claude Code install docs](https://docs.anthropic.com/en/docs/claude-code)

### Internal
- Current setup page: `docs/01-setup.md`
- Previous setup plan: `docs/plans/2026-02-17-feat-expand-setup-page-three-options-plan.md`
