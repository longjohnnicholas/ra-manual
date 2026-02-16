# Setup

<p style="font-size: 1.1rem; color: #000;">
Install VS Code and Claude Code in about 10 minutes.
</p>

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

---

## Two Ways to Use Claude Code

<div class="grid cards" markdown>

-   :material-dock-left:{ .lg .middle } __Side Panel__

    ---

    Click the Claude icon in the left sidebar. Chat interface with visual diffs when Claude edits files.

    **Best for:** Visual review, interactive debugging, exploratory sessions.

-   :material-terminal:{ .lg .middle } __Terminal__

    ---

    Type `claude` in VS Code terminal. Text-based, faster for quick queries.

    **Best for:** Quick questions, scripting, rapid iteration.

</div>

---

## Verify Installation

!!! success "Final Check"
    Open a project folder (`File → Open Folder`), then ask Claude:

    ```
    What files are in this directory?
    ```

    If Claude lists your files, you're ready. [:octicons-arrow-right-24: Next: Learn why AI coding tools are transformative](02-why-claude-code.md)
