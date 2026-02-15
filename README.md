# RA Manual

A guide for research assistants on using AI tools in research workflows.

## View the Manual

Visit the live site: **[https://ntsivanidis.github.io/ra-manual/](https://ntsivanidis.github.io/ra-manual/)**

## Deploying

This site is built with [MkDocs](https://www.mkdocs.org/) and the [Material](https://squidfunk.github.io/mkdocs-material/) theme. It deploys automatically to GitHub Pages on every push to `main`.

### Local development

```bash
pip install mkdocs-material
mkdocs serve
```

Then open [http://localhost:8000](http://localhost:8000).

### Manual deploy

```bash
mkdocs gh-deploy
```

## Structure

```
docs/
├── index.md               # Home page
├── 01-setup.md            # VS Code + Claude Code installation
├── 02-why-claude-code.md  # Why use Claude Code for research
├── 03-workflow.md         # Core workflow: plan mode, CLAUDE.md, sub-agents
├── 04-code-principles.md  # Project organization & coding standards
└── 05-resources.md        # Links and future extensions
```
