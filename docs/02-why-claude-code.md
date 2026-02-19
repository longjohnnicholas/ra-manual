# Why AI Coding Tools?

*We use Claude Code as our primary example, but these concepts apply to Codex CLI, Cursor, GitHub Copilot, and similar tools.*

The single most important thing to understand about modern AI coding tools is this: **they can see everything in your project folder**. This is what makes them fundamentally different from chatting with an AI in a browser window. When you open a folder in VS Code and start an AI assistant, it has full context — your scripts, your data dictionaries, your notes, everything.

This creates three powerful capabilities.

## 1. It Can Read and Write Your Code

Point Claude at a codebase and it becomes a collaborator. You can:

- Select a variable in a file and ask *"Where is this variable created?"*
- Say *"Write a script that cleans this dataset and runs these regressions"*
- Ask *"Explain what this script does step by step"*
- Tell it *"There's a bug in this function — the output doesn't match what I expect"*

Claude reads the relevant files, understands the context, and writes or fixes code accordingly. This isn't copy-paste from Stack Overflow — it's code that fits your specific project structure, variable names, and conventions.

## 2. It Can Use Your Research Context

This is the killer feature for research. Put supporting documents directly in your project folder:

- A `.txt` file describing your economic model
- A PDF of the paper you're replicating
- A data dictionary explaining variable definitions
- Notes on the identification strategy

Then tell Claude to read them. For example:

```
Read model_description.txt, then write a Python script that simulates
the equilibrium described in Section 3.
```

Claude will read the file, understand the model, and write simulation code that implements it. The code won't be generic — it will use the specific parameters, equations, and structure from your document.

## 3. It Can Onboard You to Unfamiliar Projects

When you inherit a project from another RA or start working on a co-author's code, open the folder and ask:

```
Describe the structure of this project. What does each script do,
and in what order should they be run?
```

Claude will read through the directory, trace the data pipeline, and give you a map of the project. This turns days of detective work into minutes.

## The Bottom Line

Claude Code turns AI from a question-answering tool into a research assistant that actually knows your project. The more context you give it (code, data descriptions, model specs), the better it performs.
