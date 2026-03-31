# Research Skills

Claude Code can run Stata or MATLAB analysis, produce figures, and write a research memo from a single prompt. Describe what you want; the agent writes the script, runs it, and delivers a reviewed write-up. You can type the instructions or speak them using Wispr. Both the PI and RAs can use these skills — the more people on the team using them, the more the team's output grows.

---

## Skills and MCP

**Skills** are instruction files that teach Claude Code how to do a task end-to-end. Invoke them with a `/` prefix — e.g., `/stata-research-assistant`. The agent handles the full pipeline: script, execution, figures, memo.

**MCP** (Model Context Protocol) connects Claude Code to Stata and MATLAB so it can run scripts, not just write them. You need one MCP server per tool — see **Installation** below.

---

## Available Skills

### Stata Research Assistant

**Invoke:** `/stata-research-assistant`

Writes a `.do` script, runs it via Stata, produces figures (300 DPI), and delivers a research memo. Use for any Stata-based analysis — regressions, data diagnostics, summary statistics.

```
/stata-research-assistant

Run a regression of log wages on education and experience using the
HFC dataset. Show me the residual plot and a summary table.
```

**Output:** `.do` script in `code/agent_sandbox/`, figures in `reports/figures/`, memo in `reports/`.

**Requires:** Stata + Stata MCP server

---

### MATLAB Research Assistant

**Invoke:** `/matlab-research-assistant`

Same workflow as Stata but for `.m` scripts. Figures use lab-standard formatting (font sizes, panel dimensions, LaTeX labels) automatically. Use for model diagnostics, estimation debugging, counterfactuals.

```
/matlab-research-assistant

Plot the estimated trade costs against distance for all country pairs.
Use log scale. Compare the baseline and counterfactual.
```

**Output:** `.m` script in the debug directory, figures in `output/figures/debug/`, memo alongside the script.

**Requires:** MATLAB + MATLAB MCP server

---

### Research Report Writer

**Invoke:** `/research-report`

Writes a memo that **synthesizes existing results** — previous scripts, literature, back-of-envelope calculations. Unlike the skills above, it doesn't run new code by default. Use it when the analysis is done and you need a clean write-up.

```
/research-report

Summarize the estimation results from the last 3 debug scripts.
Compare the wage elasticities across specifications.
```

Can run code if Stata or MATLAB MCP is installed, but doesn't require it.

---

### Memo Quality

All three skills produce memos following the same lab template:

- **Tight** — 1-2 pages, no filler
- **Self-contained** — every variable defined on first use
- **Grounded** — every claim traceable to code output, a table cell, or a figure
- **Reviewed** — a second pass checks the memo from an economics professor's perspective (up to 3 rounds)

Default output is markdown. Switches to HTML when the memo has LaTeX equations.

---

## Installation

These instructions are for macOS. If you're on Windows or Linux, paths will differ — ask the PI for help.

### 1. Clone the skills repo

```bash
git clone https://github.com/longjohnnicholas/claude-skills.git ~/Git/claude-skills
```

If the repo is private, ask the PI for access.

### 2. Install skills into Claude Code

Run these commands in Terminal to create shortcuts so Claude Code can find each skill:

```bash
cd ~/Git/claude-skills
mkdir -p ~/.claude/skills

# Link each research skill individually
ln -sfn "$(pwd)/stata-research-assistant" ~/.claude/skills/stata-research-assistant
ln -sfn "$(pwd)/report-writing/matlab-research-assistant" ~/.claude/skills/matlab-research-assistant
ln -sfn "$(pwd)/report-writing/research-report" ~/.claude/skills/research-report
```

After this, typing `/stata-research-assistant` in Claude Code will invoke the skill.

### 3. Stata MCP server

Skip if you don't use Stata. Open the file `~/.claude.json` in a text editor (it's in your home folder — `~` means home). Under `"mcpServers"`, add:

```json
"stata-mcp": {
  "type": "stdio",
  "command": "uvx",
  "args": ["--python", "3.12", "--from", "mcp-stata@latest", "mcp-stata"],
  "env": {
    "STATA_PATH": "/Applications/Stata/StataMP.app/Contents/MacOS/stata-mp",
    "MCP_STATA_SKIP_PREFLIGHT": "1"
  }
}
```

Change `STATA_PATH` to wherever Stata is installed on your machine. Requires Python 3.12 and `uvx` — if you don't have `uvx`, run `pip install uv` in Terminal.

### 4. MATLAB MCP server

Skip if you don't use MATLAB. Run in Terminal:

```bash
claude mcp add matlab-mcp --scope user -- npx -y matlab-mcp
```

Requires MATLAB on your PATH and Node.js (for `npx`).

### 5. Verify

Restart Claude Code. In a new conversation, type `/mcp` to check that `stata-mcp` and/or `matlab-mcp` appear in the server list.

### Codex

The skills repo is built for Claude Code. To use them with OpenAI's Codex CLI, the skill files may need format conversion — check with the PI.

---

## Using Wispr

Wispr lets you speak instructions instead of typing. Start Wispr dictation and describe what you want:

> "Slash stata research assistant — investigate the outliers in the wage distribution and show me a histogram."

Say "slash" before the skill name. Wispr transcribes it and Claude Code picks up the command.

---

## Tips

- **Be specific.** "Run a regression" is vague. "Regress log wages on education and experience using `hfc_clean.dta`, cluster by district" gives the agent what it needs.
- **You don't need to know the code structure.** The agent reads the codebase to find files, data paths, and variable names.
- **If the memo isn't right, say what to fix.** Direct feedback works: "Use log scale on figure 2" or "Cut the background section."
- **Verify before sharing.** The output is a first draft — check the numbers and interpretation.
