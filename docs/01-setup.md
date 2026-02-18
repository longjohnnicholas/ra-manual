# Setup

<p style="font-size: 1.1rem; color: #000;">
Pick one of three options and be coding with AI in about 10 minutes.
</p>

<div class="grid cards" markdown>

-   :material-microsoft-visual-studio-code:{ .lg .middle } __Option 1: Claude Code + VS Code__

    ---

    Anthropic's official CLI, integrated into VS Code. Requires a Claude Pro/Max/Team subscription.

    [:octicons-arrow-right-24: Jump to setup](#option-1-claude-code-vs-code)

-   :material-console:{ .lg .middle } __Option 2: Open Code + OpenRouter__

    ---

    Open-source alternative with access to 400+ models. Pay-as-you-go — use cheap models for simple tasks, expensive ones when you need them.

    [:octicons-arrow-right-24: Jump to setup](#option-2-open-code-openrouter)

-   :material-application:{ .lg .middle } __Option 3: Open Code Desktop App__

    ---

    Standalone desktop app — no VS Code required. Same model flexibility as Option 2.

    [:octicons-arrow-right-24: Jump to setup](#option-3-open-code-desktop-app)

</div>

---

## Option 1: Claude Code + VS Code

The default path. You get Anthropic's official tool with tight VS Code integration.

<div class="grid cards" markdown>

-   :material-download:{ .lg .middle } __1. Download VS Code__

    ---

    Get the IDE that powers Claude Code.

    1. Visit [code.visualstudio.com](https://code.visualstudio.com/)
    2. Download for your operating system
    3. Launch it once to verify installation

-   :material-console:{ .lg .middle } __2. Install Claude Code CLI__

    ---

    Add the command-line interface to your system.

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

    Connect Claude Code to your editor.

    1. Press `Cmd+Shift+X` (Mac) or `Ctrl+Shift+X` (Windows)
    2. Search for **"Claude Code"** by Anthropic
    3. Click **Install**

-   :material-login:{ .lg .middle } __4. Authenticate__

    ---

    Link your Anthropic account.

    In the integrated terminal, run:

    ```bash
    claude
    ```

    Sign in via browser with your Claude account (Pro, Max, Team, or Enterprise).

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

[Open Code](https://opencode.ai/) is a free, open-source AI coding agent (~106K GitHub stars, MIT license) that works with 75+ providers. Pair it with [OpenRouter](https://openrouter.ai/) and you get access to 400+ models through a single API key — including Claude, GPT, Gemini, DeepSeek, Kimi, and many free models.

### Why OpenRouter?

!!! tip "The key advantage: model flexibility"
    OpenRouter gives you **one API key** that works with models from Anthropic, OpenAI, Google, Meta, Moonshot, and dozens more. You're not locked into one provider.

    The practical benefit: **use expensive models for hard problems, cheap models for everything else.** A response that costs $0.25 with Claude Opus costs $0.02 with GPT 5.1 Codex Mini — and for simple tasks, the cheaper model works just as well.

**How it works:**

- Sign up at [openrouter.ai](https://openrouter.ai/) and create an API key
- Add credits (pay-as-you-go, no subscription)
- Point Open Code at OpenRouter — it routes your requests to whichever model you choose
- Switch models anytime with a single command

### Model Cost Comparison

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

    If you use Opus only for hard problems (maybe 10-20% of your queries) and route everything else to cheaper models, you can cut your AI costs by 60-90%.

### Step-by-Step Setup

**1. Get an OpenRouter API key**

1. Go to [openrouter.ai](https://openrouter.ai/) and create an account
2. Navigate to [Settings → Keys](https://openrouter.ai/settings/keys)
3. Click **Create API Key** and copy it
4. Add credits ($5-10 is plenty to start)

**2. Install Open Code**

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

**3. Connect OpenRouter**

Launch Open Code in your project folder:

```bash
opencode
```

Then run the `/connect` command inside Open Code, search for **OpenRouter**, and paste your API key.

<!-- screenshot: Open Code /connect command showing OpenRouter configuration -->

Alternatively, set it as an environment variable in your shell profile:

```bash
export OPENROUTER_API_KEY=sk-or-your-key-here
```

**4. Select a model**

Run `/models` inside Open Code to see all available models and pick one:

<!-- screenshot: Open Code /models command showing the model selector list -->

Or launch with a specific model directly:

```bash
opencode -m openrouter/anthropic/claude-sonnet-4-6
```

**5. (Optional) Install VS Code Extension**

Open Code has a native VS Code extension. To install:

1. Run `opencode` in the VS Code integrated terminal — the extension installs automatically
2. Or search for **"OpenCode"** in the VS Code extension marketplace

Quick launch: `Cmd+Esc` (Mac) or `Ctrl+Esc` (Windows) to open Open Code in VS Code.

### Switching Models by Task Complexity

The real power of this setup is choosing the right model for each task:

| Task | Recommended Model | Why |
|---|---|---|
| Designing a complex data pipeline | Claude Opus 4.6 or GPT 5.2 Codex | Needs deep reasoning |
| Writing a new regression script | Claude Sonnet 4.6 | Good balance of quality and cost |
| Explaining what a script does | Claude Haiku 4.5 | Fast, cheap, good enough |
| Fixing a typo or renaming variables | GPT 5.1 Codex Mini | Trivial task, use the cheapest option |
| Exploring a new codebase | Kimi K2.5 | Cheap with a huge 262K context window |

**To switch models during a session**, run `/models` and pick a different one. To set a default for everyday work, add this to your `opencode.json` config file:

```json
{
  "model": "openrouter/anthropic/claude-sonnet-4-6",
  "small_model": "openrouter/openai/gpt-5.1-codex-mini"
}
```

This uses Sonnet as your primary model and Codex Mini for lightweight tasks automatically.

---

## Option 3: Open Code Desktop App

If you don't want to use VS Code at all, Open Code has a standalone desktop app (currently in Beta).

<!-- screenshot: Open Code desktop app showing the main interface -->

**1. Download and install**

=== "Mac (Homebrew)"

    ```bash
    brew install --cask opencode-desktop
    ```

=== "Mac / Windows / Linux"

    Download from [opencode.ai/download](https://opencode.ai/download)

**2. Configure OpenRouter**

Same process as Option 2 — run `/connect`, search for OpenRouter, paste your API key. You get the same model selection and cost benefits.

**3. Open a project folder and start coding**

!!! info "When to use the desktop app"
    The desktop app is a good choice if:

    - You prefer a dedicated window over VS Code
    - You primarily work in the terminal and want a lightweight AI companion
    - You want the simplest possible setup (download one app, add one API key)

    It supports the same features as the terminal version: model switching, MCP tools, file editing, and session management.

---

## Verify Installation

!!! success "Final Check"
    Whichever option you chose, verify it works:

    === "Claude Code"

        Open a project folder in VS Code and ask:

        ```
        What files are in this directory?
        ```

    === "Open Code (Terminal or VS Code)"

        Navigate to a project folder and run:

        ```bash
        opencode
        ```

        Then ask:

        ```
        What files are in this directory?
        ```

    === "Open Code Desktop"

        Open a project folder in the app and ask:

        ```
        What files are in this directory?
        ```

    If the AI lists your files, you're ready. [:octicons-arrow-right-24: Next: Learn why AI coding tools are transformative](02-why-claude-code.md)
