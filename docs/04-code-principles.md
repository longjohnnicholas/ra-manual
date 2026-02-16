# Project Organization & Coding Principles

These are the lab's standards for organizing research projects. Following them makes your code readable, reproducible, and Claude-friendly.

## Repository Structure

Repositories are organized by task type at the top level, with subfolders for specific datasets or analyses. Each subfolder contains its own `code/`, `temp/`, `output/`, and `README`.

```
repo_name/
├── .gitignore          # One .gitignore at repo root (not in subfolders)
├── raw/                # Raw data (read-only, never modified)
├── cleaning/
│   ├── survey_data/
│   │   ├── code/       # Scripts + CLAUDE.md lives here
│   │   ├── temp/       # Intermediate files (gitignored)
│   │   ├── output/     # Cleaned datasets
│   │   └── README.md
│   └── admin_data/
│       ├── code/
│       ├── temp/
│       ├── output/
│       └── README.md
├── analysis/
│   ├── main_regressions/
│   │   ├── code/
│   │   ├── temp/
│   │   ├── output/
│   │   └── README.md
│   └── robustness/
│       ├── code/
│       ├── temp/
│       ├── output/
│       └── README.md
└── figures/
    └── main_figures/
        ├── code/
        ├── temp/
        ├── output/
        └── README.md
```

**Key points:**

- **One `.gitignore` at the repo root** — not in every subfolder
- **Claude materials (`CLAUDE.md`) go inside `code/`** for each task — we don't always use Claude, so keep AI config with the scripts
- **Each task subfolder is self-contained** with its own `code/`, `temp/`, `output/`, and `README`

Your root `.gitignore` should include:

```
**/temp/
*.dta
*.csv
*.log
.DS_Store
```

## Number Your Scripts

Prefix every script with a number indicating its order in the pipeline:

```
code/
├── 1_load_raw.do
├── 2_clean_variables.do
├── 3_merge_datasets.do
└── 4_export_cleaned.do
```

This makes execution order immediately obvious to anyone reading the project — including Claude. When someone opens the folder, they can see at a glance what runs first, second, third.

For sub-steps, use letters: `1a_clean_trade.do`, `1b_clean_firms.do`.

## Functional Programming

Write functions, not monolithic scripts. Every script should be a collection of well-named functions that each do one thing.

**Bad** — a 500-line script that loads data, cleans it, runs regressions, and makes tables all in one go.

**Good** — a main script that calls discrete functions:

```python
# 3_run_regressions.py

def load_analysis_data(path):
    """Load the cleaned analysis dataset."""
    ...

def run_main_specification(df):
    """Run the baseline OLS regression (Table 1, Column 1)."""
    ...

def run_iv_specification(df, instrument):
    """Run the IV regression (Table 1, Column 3)."""
    ...

if __name__ == "__main__":
    df = load_analysis_data("output/cleaning/analysis_sample.parquet")
    ols_results = run_main_specification(df)
    iv_results = run_iv_specification(df, instrument="bartik_shock")
    export_table(ols_results, iv_results, path="output/analysis/table1.tex")
```

This approach is better for three reasons: each function can be tested independently, Claude can understand and modify individual functions without breaking others, and you can reuse functions across scripts.

The same principle applies in Stata — use programs and ado files rather than one continuous script.

## Version Control

- Commit early, commit often. Every meaningful change should be a commit.
- Write descriptive commit messages: *"Add IV regression with Bartik instrument"* not *"update code"*.
- Never commit data files, temporary outputs, or credentials.
- Keep `README.md` up to date — it should describe how to run the full pipeline from scratch.

## Additional Principles

**Relative paths only.** Never hardcode absolute paths like `/Users/nick/Dropbox/...`. Use paths relative to the project root. This ensures the project runs on any machine.

**One master script.** Every project should have a single script (e.g., `run_all.do` or `Makefile`) that executes the entire pipeline from raw data to final output. If someone can't reproduce your results by running one command, the project isn't properly organized.

**Separate data from code.** Raw data should live in a `data/` folder (or be downloaded by a script). Never modify raw data files — treat them as read-only. All transformations happen in code and output to `temp/` or `output/`.

**Comment the why, not the what.** Don't write `# add 1 to x` — write `# adjust for zero-indexing in the census year variable`. Claude can read what the code does; it needs to know *why* you're doing it.
