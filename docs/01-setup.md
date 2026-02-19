# Setup

<p style="font-size: 1.1rem;">
Install VS Code, pick your AI agent, and be coding in about 10 minutes.
</p>

<div class="grid cards" markdown>

-   :material-robot-outline:{ .lg .middle } __Option A: Claude Code__

    ---

    Anthropic's official CLI agent. Requires a Claude Pro, Max, or Team subscription.

    [:octicons-arrow-right-24: Jump to setup](#option-a-claude-code)

-   :material-robot-happy-outline:{ .lg .middle } __Option B: Codex CLI__

    ---

    OpenAI's official CLI agent. Requires a ChatGPT Plus, Pro, or Team subscription.

    [:octicons-arrow-right-24: Jump to setup](#option-b-codex-cli)

</div>

---

## Step 1: Install VS Code

Both AI agents run inside VS Code. Install it first.

1. Visit [code.visualstudio.com](https://code.visualstudio.com/)
2. Download for your operating system
3. Launch it once to verify installation

!!! note "Why VS Code?"
    VS Code is your workbench — it hosts the AI agent, your code editor, the terminal, and extensions for tools like Stata. Both Claude Code and Codex CLI integrate as a sidebar panel *and* as a terminal command inside VS Code.

---

## Step 2: Pick Your AI Agent

Choose the agent that matches your subscription. Both are equally capable for research tasks.

!!! tip "Which should I pick?"
    - Already have a **Claude** subscription? → [Option A](#option-a-claude-code)
    - Already have a **ChatGPT** subscription? → [Option B](#option-b-codex-cli)
    - Neither? Ask your advisor which the team uses.
    - Both work equally well. You can install both if you want to try each.

    **If your advisor is providing the subscription**, ask them to add your email to the team workspace before you begin.

---

### Option A: Claude Code

The official Anthropic agent. Requires a Claude Pro ($20/mo), Max ($100/mo), or Team subscription.

<div class="grid cards" markdown>

-   :material-console:{ .lg .middle } __1. Install the CLI__

    ---

    === "Mac / Linux"

        ```bash
        curl -fsSL https://claude.ai/install.sh | bash
        ```

    === "Windows (PowerShell)"

        ```powershell
        irm https://claude.ai/install.ps1 | iex
        ```

    === "Homebrew (Mac)"

        ```bash
        brew install --cask claude-code
        ```

    Verify with: `claude --version`

-   :material-puzzle:{ .lg .middle } __2. Install the VS Code Extension__

    ---

    1. Press `Cmd+Shift+X` (Mac) or `Ctrl+Shift+X` (Windows)
    2. Search for **"Claude Code"** by Anthropic
    3. Click **Install**

-   :material-login:{ .lg .middle } __3. Authenticate__

    ---

    In the VS Code terminal, run:

    ```bash
    claude
    ```

    A browser window opens — sign in with your Claude account.

</div>

Use Claude from the **sidebar panel** (click the Claude icon) or the **terminal** (type `claude`). Both give you the same agent.

---

### Option B: Codex CLI

OpenAI's official agent. Requires a ChatGPT Plus ($20/mo), Pro ($200/mo), or Team subscription. Plus is sufficient for most RA work.

<div class="grid cards" markdown>

-   :material-console:{ .lg .middle } __1. Install the CLI__

    ---

    === "Homebrew (Mac)"

        ```bash
        brew install --cask codex
        ```

    === "npm (Mac / Linux / Windows)"

        Requires [Node.js](https://nodejs.org/) — download the LTS version if you don't have it.

        ```bash
        npm i -g @openai/codex
        ```

    === "Windows (PowerShell)"

        Install [Node.js](https://nodejs.org/) first, then run in PowerShell:

        ```powershell
        npm i -g @openai/codex
        ```

    Verify with: `codex --version`

-   :material-puzzle:{ .lg .middle } __2. Install the VS Code Extension__

    ---

    1. Press `Cmd+Shift+X` (Mac) or `Ctrl+Shift+X` (Windows)
    2. Search for **"ChatGPT"** by OpenAI
    3. Click **Install**

-   :material-login:{ .lg .middle } __3. Authenticate__

    ---

    In the VS Code terminal, run:

    ```bash
    codex
    ```

    A browser window opens — sign in with your ChatGPT account.

</div>

Use Codex from the **sidebar panel** (click the ChatGPT icon) or the **terminal** (type `codex`). Both give you the same agent.

---

## Verify Installation

!!! success "Final Check"
    Whichever option you chose, open a project folder in VS Code and ask:

    ```
    What files are in this directory?
    ```

    If the AI lists your files, you're ready. [:octicons-arrow-right-24: Next: Learn why AI coding tools are transformative](02-why-claude-code.md)
