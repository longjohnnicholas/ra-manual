# Research Skills

Claude Code and Codex can do more than write code. With the right skills installed, you can tell them to run analysis in Stata or MATLAB, produce publication-quality figures, and write a research memo — all from a single prompt. You can type the instructions or speak them using Wispr.

---

## What Are Skills?

Skills are instruction files that teach Claude Code (or Codex) how to do a specific task end-to-end. You invoke them with a `/` prefix — for example, `/stata-research-assistant`. When you invoke a skill, the agent follows a structured workflow: it reads your code, writes a script, runs it, produces figures, writes a memo, fact-checks it, and reviews it — then delivers everything to you.

---

## What Is MCP?

MCP (Model Context Protocol) connects Claude Code to external software like Stata and MATLAB. Without MCP, Claude can write scripts but can't run them. With the Stata MCP server installed, Claude can execute `.do` files directly and read the output. Same for MATLAB. Think of MCP as plugging Claude into your analysis tools. You need to install an MCP server for each tool you want Claude to use — see **Installation** below.

---

## Available Skills

### Stata Research Assistant

**Invoke with:** `/stata-research-assistant`

**What it does:** Runs a complete research workflow — writes a `.do` debug script, executes it via Stata, produces figures at 300 DPI, writes a research memo following the lab template, fact-checks every claim, and runs a reviewer sub-agent (up to 3 rounds). Delivers the script, figures, and memo.

**When to use:** Investigating data patterns, running regressions, debugging Stata code, producing summary statistics or diagnostics.

**Example prompt:**

```
/stata-research-assistant

Run a regression of log wages on education and experience using the
HFC dataset. Show me the residual plot and a summary table.
Save everything to a memo.
```

**What you get:**

- A `.do` script in `code/agent_sandbox/`
- Figures in `code/agent_sandbox/reports/figures/`
- A self-contained research memo in `code/agent_sandbox/reports/`

**Requires:** Stata installed + Stata MCP server (see Installation)

---

### MATLAB Research Assistant

**Invoke with:** `/matlab-research-assistant`

**What it does:** Same workflow structure as Stata — writes a `.m` debug script, runs it via MATLAB, produces publication-quality figures (with lab-standard font sizes, panel dimensions, and LaTeX labels), writes a memo, fact-checks, and reviews. The agent handles all figure formatting automatically.

**When to use:** Investigating model behavior, debugging estimation, running counterfactuals, producing diagnostics.

**Example prompt:**

```
/matlab-research-assistant

Plot the estimated trade costs against distance for all country pairs.
Use log scale. Compare the baseline and counterfactual.
```

**What you get:**

- A `.m` script in the debug directory
- Figures in `output/figures/debug/`
- A research memo alongside the script

**Requires:** MATLAB installed + MATLAB MCP server (see Installation)

---

### Research Report Writer

**Invoke with:** `/research-report`

**What it does:** Writes a polished research memo on any question using whatever tools fit the task — Stata, MATLAB, Python, R, or just reading existing code and data. Follows the same lab template. Fact-checks and reviews.

**When to use:** You need a clean internal report — data analysis, model diagnostics, literature summary, back-of-envelope calculation, or comparing results across specifications.

**Example prompt:**

```
/research-report

Summarize the estimation results from the last 3 debug scripts.
Compare the wage elasticities across specifications.
```

**Note:** This skill is language-agnostic. It doesn't require a specific MCP server, but benefits from having Stata or MATLAB MCP installed if the analysis needs to run code.

---

### The Shared Template

All three skills follow the same research memo template. Every memo produced by these skills is:

- **Tight** — 1-2 pages, every section earned, no filler
- **Self-contained** — every variable defined on first use
- **Grounded** — every claim traceable to code output, a table cell, or a figure
- **Reviewed** — a sub-agent reviews from an economics professor's perspective (up to 3 rounds)

Output format is markdown by default. If the memo has more than 2 LaTeX equations, it automatically switches to a self-contained HTML file with proper math rendering.

---

## Installation

### 1. Clone the skills repo

```bash
git clone https://github.com/longjohnnicholas/claude-skills.git ~/Git/claude-skills
```

If the repo is private, ask the PI for access first.

### 2. Install skills into Claude Code

```bash
cd ~/Git/claude-skills
mkdir -p ~/.claude/skills
for skill in */; do
  base=$(basename "$skill")
  ln -sfn "$(pwd)/$skill" ~/.claude/skills/$base
done
```

This creates symlinks so Claude Code can find the skills when you type `/skill-name`.

### 3. Install the Stata MCP server

Skip this if you don't use Stata.

Open the file `~/.claude.json` in a text editor. Under `"mcpServers"`, add:

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

Change `STATA_PATH` to wherever Stata is installed on your machine. This requires Python 3.12 and `uvx` — if you don't have `uvx`, install it with `pip install uv`.

### 4. Install the MATLAB MCP server

Skip this if you don't use MATLAB.

```bash
claude mcp add matlab-mcp --scope user -- npx -y matlab-mcp
```

This requires MATLAB installed with `matlab` on your PATH, and Node.js (for `npx`).

### 5. Verify

Restart Claude Code, then type `/mcp` to check that Stata and/or MATLAB tools appear in the list.

### Using with Codex

The skills repo is built for Claude Code. To use skills with OpenAI's Codex CLI, the skill files may need format conversion. Check with the PI for current status on Codex compatibility.

---

## Using Wispr

Wispr lets you speak your instructions instead of typing. Open Claude Code, start Wispr dictation, and describe what you want:

> "Slash stata research assistant — investigate the outliers in the wage distribution and show me a histogram."

The skill name is spoken as "slash" followed by the skill name. Wispr transcribes it and Claude Code picks up the `/` command.

---

## Tips

- **Be specific.** Name the variables, the dataset, and the output format you want. "Run a regression" is vague — "Regress log wages on education and experience using `hfc_clean.dta`, cluster by district" gives the agent what it needs.
- **You don't need to know the code structure.** The agent reads the codebase to find the right files, data paths, and variable names.
- **The agent asks clarifying questions** if your instructions are ambiguous — just answer them.
- **If the memo isn't right, say what to fix.** The agent iterates with a reviewer for up to 3 rounds. You can also give it direct feedback: "The second figure should use log scale" or "Cut the background section."
- **Check the output.** These skills produce good first drafts, but always verify the numbers, figures, and interpretation before sharing.
