# Setup

<p style="font-size: 1.1rem; color: #000;">
Pick one of two options and be coding with AI in about 10 minutes.
</p>

<div class="grid cards" markdown>

-   :material-robot-outline:{ .lg .middle } __Option 1: Claude Code__

    ---

    Anthropic's official CLI, integrated into VS Code. Requires a Claude Pro/Max/Team subscription.

    [:octicons-arrow-right-24: Jump to setup](#option-1-claude-code)

-   :material-swap-horizontal:{ .lg .middle } __Option 2: Open Code + OpenRouter__

    ---

    Open-source alternative with access to 400+ models. Use cheap models for simple tasks, expensive ones when you need them. Ask Nick for the API key.

    [:octicons-arrow-right-24: Jump to setup](#option-2-open-code-openrouter)

</div>

---

## Option 1: Claude Code

The official Anthropic tool with tight VS Code integration. You need a Claude Pro, Max, Team, or Enterprise subscription.

<div class="grid cards" markdown>

-   :material-download:{ .lg .middle } __1. Download VS Code__

    ---

    1. Visit [code.visualstudio.com](https://code.visualstudio.com/)
    2. Download for your operating system
    3. Launch it once to verify installation

-   :material-console:{ .lg .middle } __2. Install Claude Code CLI__

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

-   :material-puzzle:{ .lg .middle } __3. Install VS Code Extension__

    ---

    1. Press `Cmd+Shift+X` (Mac) or `Ctrl+Shift+X` (Windows)
    2. Search for **"Claude Code"** by Anthropic
    3. Click **Install**

-   :material-login:{ .lg .middle } __4. Authenticate__

    ---

    In the integrated terminal, run:

    ```bash
    claude
    ```

    Sign in via browser with your Claude account.

</div>

### Two Ways to Use Claude Code

<div class="grid cards" markdown>

-   :material-dock-window:{ .lg .middle } __Side Panel__

    ---

    Click the Claude icon in the left sidebar. Chat interface with visual diffs when Claude edits files.

    **Best for:** Visual review, interactive debugging, exploratory sessions.

-   :material-console-line:{ .lg .middle } __Terminal__

    ---

    Type `claude` in VS Code terminal. Text-based, faster for quick queries.

    **Best for:** Quick questions, scripting, rapid iteration.

</div>

---

## Option 2: Open Code + OpenRouter

[Open Code](https://opencode.ai/) is a free, open-source AI coding agent (~106K GitHub stars, MIT license). Pair it with [OpenRouter](https://openrouter.ai/) and you get access to **400+ models** through a single API key — Claude, GPT, Gemini, DeepSeek, Kimi, and many more.

### Why OpenRouter?

!!! note "Ask Nick for the API key"
    You don't need to create an account or add any money. **Ask Nick for the team's OpenRouter API key** and keep it somewhere safe — you'll need it in step 2.

[OpenRouter](https://openrouter.ai/) gives you **one API key** that works with models from Anthropic, OpenAI, Google, Meta, Moonshot, and dozens more. You're not locked into one provider.

The key advantage: **use expensive models for hard problems, cheap models for everything else.** A response that costs $0.25 with Claude Opus costs $0.02 with GPT 5.1 Codex Mini — and for simple tasks, the cheaper model works just as well.

#### Model Cost Comparison

Prices per **million tokens** (as of February 2026 — check [openrouter.ai/models](https://openrouter.ai/models) for current pricing):

| Model | Input | Output | When to Use |
|---|---|---|---|
| **Claude Opus 4.6** | $5.00 | $25.00 | Complex architecture, novel reasoning |
| **Claude Sonnet 4.6** | $3.00 | $15.00 | Balanced quality and cost |
| **GPT 5.2 Codex** | $1.75 | $14.00 | Strong coding, cheaper than Opus |
| **Claude Haiku 4.5** | $1.00 | $5.00 | Quick tasks, code review, explanations |
| **Kimi K2.5** | $0.23 | $3.00 | Budget coding with 262K context |
| **GPT 5.1 Codex Mini** | $0.25 | $2.00 | Simple/bulk coding tasks |
| **DeepSeek V3.2** | $0.25 | $0.38 | Near-free coding |
| **MiMo-V2-Flash** | FREE | FREE | Experimentation, simple tasks |

!!! example "What this means in practice"
    A typical AI coding response is about 10,000 output tokens. That costs:

    - **Claude Opus 4.6:** ~$0.25
    - **Claude Haiku 4.5:** ~$0.05
    - **GPT 5.1 Codex Mini:** ~$0.02
    - **DeepSeek V3.2:** less than $0.01

    Use Opus only for hard problems (maybe 10-20% of your queries) and route everything else to cheaper models. This can cut costs by 60-90%.

### Step-by-Step Setup

**1. Install Open Code**

=== "Mac / Linux"

    ```bash
    curl -fsSL https://opencode.ai/install | bash
    ```

=== "Homebrew (Mac)"

    ```bash
    brew install anomalyco/tap/opencode
    ```

=== "npm"

    ```bash
    npm i -g opencode-ai
    ```

=== "Windows (Scoop)"

    ```powershell
    scoop install opencode
    ```

**2. Connect OpenRouter**

Launch Open Code in any folder:

```bash
opencode
```

Then run the `/connect` command inside Open Code, search for **OpenRouter**, and paste the API key Nick gave you.

<!-- screenshot: Open Code /connect command showing OpenRouter configuration -->

Alternatively, set it as an environment variable in your shell profile (e.g., `~/.zshrc` or `~/.bashrc`):

```bash
export OPENROUTER_API_KEY=sk-or-your-key-here
```

**3. Select a model**

Run `/models` inside Open Code to see all available models and pick one:

<!-- screenshot: Open Code /models command showing the model selector list -->

Or launch with a specific model directly:

```bash
opencode -m openrouter/anthropic/claude-sonnet-4-6
```

**4. Switching models by task complexity**

This is the real power of this setup — choose the right model for each task:

| Task | Recommended Model | Why |
|---|---|---|
| Designing a complex data pipeline | Claude Opus 4.6 or GPT 5.2 Codex | Needs deep reasoning |
| Writing a new regression script | Claude Sonnet 4.6 | Good balance of quality and cost |
| Explaining what a script does | Claude Haiku 4.5 | Fast, cheap, good enough |
| Fixing a typo or renaming variables | GPT 5.1 Codex Mini | Trivial task, use the cheapest option |
| Exploring a new codebase | Kimi K2.5 | Cheap with a huge 262K context window |

To switch models during a session, run `/models` and pick a different one. To set defaults, add this to your `opencode.json` config file:

```json
{
  "model": "openrouter/anthropic/claude-sonnet-4-6",
  "small_model": "openrouter/openai/gpt-5.1-codex-mini"
}
```

**5. Choose your editor**

<div class="grid cards" markdown>

-   :material-microsoft-visual-studio-code:{ .lg .middle } __Option A: Terminal + VS Code__

    ---

    Use Open Code inside VS Code — the same editor used across most research teams.

    [:octicons-arrow-right-24: Set up VS Code](#option-a-terminal-vs-code)

-   :material-application:{ .lg .middle } __Option B: Open Code Desktop App__

    ---

    Standalone app — no VS Code needed. Lightweight, simple, same features.

    [:octicons-arrow-right-24: Set up Desktop App](#option-b-open-code-desktop-app)

</div>

#### Option A: Terminal + VS Code

**1. Download VS Code**

1. Visit [code.visualstudio.com](https://code.visualstudio.com/)
2. Download for your operating system
3. Launch it once to verify installation

**2. Install the Open Code Extension**

Either:

- Run `opencode` in the VS Code integrated terminal — the extension installs automatically
- Or press `Cmd+Shift+X` (Mac) / `Ctrl+Shift+X` (Windows), search for **"OpenCode"**, and click **Install**

**3. Start using it**

Open a project folder in VS Code, then:

- **Quick launch:** `Cmd+Esc` (Mac) or `Ctrl+Esc` (Windows)
- **Or:** type `opencode` in the VS Code terminal

#### Option B: Open Code Desktop App

A standalone desktop app — currently in Beta, built with Tauri (lightweight and native).

<!-- screenshot: Open Code desktop app showing the main interface -->

**1. Download and install**

=== "Mac (Homebrew)"

    ```bash
    brew install --cask opencode-desktop
    ```

=== "Mac / Windows / Linux"

    Download from [opencode.ai/download](https://opencode.ai/download)

**2. Open a project folder and start coding**

The desktop app uses the same OpenRouter connection you set up in steps 2-3. No extra setup needed.

!!! info "When to use the desktop app"
    The desktop app is a good choice if:

    - You prefer a dedicated window over VS Code
    - You primarily work in the terminal and want a lightweight AI companion
    - You want the simplest possible setup

---

## Verify Installation

!!! success "Final Check"
    Whichever option you chose, open a project folder and ask:

    ```
    What files are in this directory?
    ```

    If the AI lists your files, you're ready. [:octicons-arrow-right-24: Next: Learn why AI coding tools are transformative](02-why-claude-code.md)
