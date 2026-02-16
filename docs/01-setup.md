# Setup

This page walks you through installing VS Code and Claude Code. The whole process takes about 10 minutes.

## 1. Install VS Code

Download Visual Studio Code from [code.visualstudio.com](https://code.visualstudio.com/) and install it for your operating system. Open it once to make sure it launches.

## 2. Install the Claude Code CLI

Open a terminal (on Mac: Terminal.app or the VS Code integrated terminal) and run the installer:

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

After installation, verify it works:

```bash
claude --version
```

## 3. Install the VS Code Extension

1. Open VS Code
2. Press `Cmd+Shift+X` (Mac) or `Ctrl+Shift+X` (Windows/Linux) to open the Extensions panel
3. Search for **"Claude Code"** (by Anthropic)
4. Click **Install**

## 4. Log In

Open the VS Code integrated terminal (`Cmd+`` ` on Mac, `` Ctrl+` `` on Windows) and run:

```bash
claude
```

This will open a browser window to authenticate. Log in with your Anthropic account (Claude Pro, Max, Team, or Enterprise). You only need to do this once.

## 5. Two Ways to Use Claude Code

You now have two ways to interact with Claude inside VS Code:

**Side panel**: Click the Claude icon in the left sidebar. This gives you a chat-style interface with visual diffs when Claude edits files.

![Claude Code side panel in VS Code](images/vscode-sidepanel.png)

**Terminal**: Open the integrated terminal and type `claude`. This gives you a text-based interface — faster for quick questions and scripting.

![Claude Code in the VS Code terminal](images/vscode-terminal.png)

Both are equivalent in capability. Use whichever feels more natural.

## 6. Verify It Works

Open a project folder in VS Code (`File → Open Folder`), then ask Claude:

```
What files are in this directory?
```

If Claude lists your files, you're good to go. Move on to the next section.
