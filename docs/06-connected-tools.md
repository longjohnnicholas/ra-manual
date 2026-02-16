# Connected External Tools: Google Drive, Gmail, and More

One of the most powerful things about incorporating AI into your research workflow is that it goes far beyond writing code. You can connect Claude to external services — Google Drive, Gmail, Google Sheets, and others — and automate operational tasks that previously required hours of manual work.

This is especially valuable in fieldwork, where the volume of reports, data checks, and communications can overwhelm even a well-organized team.

## What Are MCP Connectors?

MCP (Model Context Protocol) is a standard that lets Claude talk to external services. An MCP connector is a small bridge that gives Claude the ability to read your Google Drive files, search your Gmail, pull data from Google Sheets, and more — all from within Claude Code.

Think of it this way: without MCP, Claude can only see files in your local project folder. With MCP connectors, Claude can reach into your Drive, your inbox, and other tools as if they were part of the project.

Setting up a connector typically involves installing a small package and authenticating with the service (e.g., logging into your Google account). Once connected, you can ask Claude to interact with these services in natural language.

## Example: Automating Fieldwork Quality Control

Here's a real use case from our lab that illustrates why this matters.

### The Problem

During a field survey, quality control generates a flood of information that someone needs to review:

- **Supervisor reports** — qualitative summaries submitted by field supervisors, stored as Google Docs on Drive. These describe how enumeration went, flag issues with specific enumerators, and note logistical problems.

- **High-frequency check tables** — statistical outputs produced by Stata (e.g., response rates, duration checks, logical consistency flags), saved as Excel files on Drive. These tables can be large and dense — dozens of enumerators across dozens of metrics.

- **Email traffic** — messages from the field team that may contain urgent flags, updates, or issues that need attention.

Previously, an RA would need to open each supervisor report, read through it, cross-reference with the HFC tables, scan relevant emails, and then produce a summary. This could take hours, and it had to happen regularly — sometimes daily during active data collection.

### The Solution

With MCP connectors, you can build Claude skills that automate this entire pipeline:

1. **Connect to Google Drive** — Claude reads the latest supervisor reports and HFC tables directly from your shared Drive folder.
2. **Connect to Gmail** — Claude scans recent emails from the field team for flags or issues.
3. **Cross-reference and analyze** — Claude reads through the qualitative reports, extracts key issues, matches them against the quantitative HFC flags, and checks email for corroborating information.
4. **Produce a summary report** — Claude generates a structured briefing that categorizes enumerators by severity:
    - *Major issues* — enumerators who need immediate attention or a conversation with the supervisor
    - *Minor issues* — enumerators who need targeted feedback to improve
    - *All clear* — enumerators performing within acceptable parameters

What used to take an RA several hours now runs in minutes. The RA's role shifts from data processing to decision-making — reviewing Claude's summary and deciding what action to take.

### Working Examples

Our lab has built skills that implement this workflow. You can find them in the project repository:

:material-github: **[freetown/tools/claude](https://github.com/ntsivanidis/freetown/tree/main/tools/claude)** — Contains working Claude Code skills that connect to Google Drive and Gmail for fieldwork quality control. These skills read supervisor reports, parse HFC tables, and produce actionable summary reports.

Study these examples to understand how MCP skills are structured, then adapt them for your own project's needs.

## Other Use Cases

The Drive + Gmail pattern generalizes to many research operations:

- **Literature monitoring** — Connect to Gmail and have Claude scan for new working paper alerts from NBER, SSRN, or journal feeds, then summarize the relevant ones.
- **Data delivery tracking** — When a data provider sends files to a shared Drive folder, have Claude detect new arrivals, run basic validation checks, and notify you.
- **Survey instrument review** — Store survey drafts on Drive and have Claude review them for consistency, skip logic errors, or translation issues.
- **Meeting preparation** — Have Claude scan recent emails and Drive documents related to a co-author meeting and produce a summary of open items.

## Getting Started with MCP Connectors

To connect Claude Code to Google Drive and Gmail, you'll need to set up MCP servers. The basic process:

1. **Install the MCP server package** for the service you want (e.g., Google Drive, Gmail)
2. **Authenticate** — follow the OAuth flow to grant Claude access to your account
3. **Configure Claude Code** — add the MCP server to your Claude Code settings so it's available in your sessions
4. **Build skills** — write skills (in `.claude/skills/`) that use the connected services

For detailed setup instructions and working examples, see the [freetown/tools/claude](https://github.com/ntsivanidis/freetown/tree/main/tools/claude) repository.

!!! note
    MCP connectors require careful attention to data access permissions. Only connect services that contain data you're comfortable having Claude read. For projects with sensitive or restricted-use data, consult your PI before setting up connectors.
