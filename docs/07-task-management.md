# Task Management with Linear

The lab tracks work in Linear. A **project** is a push of work with a clear goal — *Prepare materials for survey round 2*, *Develop and deploy HFC*. An **issue** is one task inside a project, assigned to one person. Move your issue's status when your work status changes — that's how the PI tracks progress without having to ask.

---

## Getting into Linear

Linear has a desktop app and a web app. **Use the desktop app** — it's faster and sends notifications you'll miss otherwise. Download it at [linear.app/download](https://linear.app/download). The web app at [linear.app](https://linear.app) works if you can't install anything.

The PI will invite you via email. Once you're in, you'll see the lab's **teams** in the left sidebar — each research project has its own team. Click a team to see its issues. If you haven't received an invite, ask the PI.

Linear is keyboard-first. Most actions have a shortcut — you'll pick these up fast.

---

## Finding Your Work

Press **`G` then `M`** to go to **My Issues** — this shows everything assigned to you across all projects.

To see issues where you are the **reviewer**, filter by label: open any team view, press `F` to add a filter, select **Label**, and choose your `Reviewer: [name]` label. This shows all issues waiting for your review.

---

## Projects and Issues

**Projects** are pushes of work — a defined effort with a clear goal and end date. Examples:

- *Prepare materials for survey round 2*
- *Develop and deploy HFC*
- *Clean enumeration zone data*

**Issues** are the individual tasks inside a project. Each issue has one person doing it, a reviewer, a status, and a description explaining what needs to be done.

### Creating an issue

Press **`C`** to create a new issue. Fill in:

- **Title** — what the task is
- **Assignee** — the person doing the work (`A` to set)
- **Reviewer label** — add a label `Reviewer: name`, e.g. `Reviewer: ntsivanidis` (`L` to open labels). **The automated reviewer uses this to know who does the human review.** If you skip it, the agent will bounce the issue back.
- **Project** — which project this belongs to (`⇧P` to set)

The issue description should have three sections: `## Objective`, `## Acceptance Criteria`, and `## Deliverable Links`. The PI usually fills in the first two when creating the task. If they're blank, write them yourself — the agent will bounce the issue if they're missing.

### Issue statuses

Each issue has a status. Change it by clicking the status field and selecting from the dropdown.

| Status | What it means | Who moves it |
|--------|--------------|-------------|
| **Backlog** | Queued, not yet started | PI |
| **Assigned** | Yours to do | PI |
| **In Progress** | You're actively working on it | You — as soon as you start |
| **Agent Review** | Finished — ready for review | You — when work is complete |
| **Revisions Needed** | Agent or PI found issues | Automatic — fix and resubmit |
| **Human Review** | Agent approved, PI reviewing | Automatic |
| **Done** | Work accepted | PI |

Move the issue when your status changes. If it sits in "Assigned" while you're two days in, the PI has no visibility.

---

## The Review Timeline

When your work is complete, change the issue's status to **Agent Review**. An automated AI reviewer reads your work and checks it against the objective and acceptance criteria.

```
In Progress
     |
     | (work complete — change status to Agent Review)
     v
Agent Review ──[blocking issues]──> Revisions Needed
     |                                      |
[no blocking issues]              You fix + resubmit
     |                                      |
     v                                      v
Human Review <──────────────────── Agent Review (round 2)
     |                                      |
     v                          [still blocking after 2 rounds]
   Done                                     |
                                            v
                                     Human Review
                                    (auto-escalated)
```

The agent reviews up to **2 rounds**. After that it escalates to Human Review — the PI decides.

After fixing revisions, move the issue back to **Agent Review** or post `/review` as a comment on the issue.

You can skip the agent at any point by posting `/escalate` as a comment on the issue.

---

## Before Submitting for Review

Three things before you change the status to Agent Review:

### 1. Fill in the issue description

Make sure the description has these three sections:

- **`## Objective`** — one sentence: what should this work achieve?
- **`## Acceptance Criteria`** — bullets: what does "done" look like?
- **`## Deliverable Links`** — the URL to your GitHub PR, commit, or Google Doc

The PI usually writes the Objective and Acceptance Criteria when they create the task. Don't rewrite them — just add your Deliverable Link. If they're blank, fill them in yourself.

```
## Objective
Clean the enumeration zone shapefile and produce a map for PI review.

## Acceptance Criteria
- Shapefile loads cleanly in R and Stata
- Map shows all EZs with district labels
- README updated with data source and date

## Deliverable Links
https://github.com/org/lagos-danfo/commit/abc1234...
```

The link can be a GitHub commit URL, PR URL, or Google Doc URL.

### 2. Add a Reviewer label

On the issue, find the **Labels** field (in the right-hand properties panel) and add a label in the format `Reviewer: name` — for example, `Reviewer: ntsivanidis`. If the label doesn't exist yet, create it from the labels panel.

### 3. Post a Summary comment

Scroll to the comments and post using this template:

```
**Summary** @[reviewer name]

**Task Purpose:** What the task was about (1-2 sentences).

**Procedure:** What you did (up to 5 sentences).

**Output Location:** Where to find the output. Include the final commit URL.

**Additional Notes:** Anything else relevant.
```

Replace `@[reviewer name]` with the name from your Reviewer label. The summary must include a GitHub commit or PR URL — the agent checks for this before reviewing.

You only need the Summary on your first submission. On re-reviews after revisions, just post your fix response.

---

## What the Agent Reviews

The agent reads what you linked: the diff of your code changes (GitHub PR or commit) or the full text of a Google Doc. It checks your work against the Objective and Acceptance Criteria and produces a structured review.

Findings are tagged either `[Blocking]` (must fix to pass) or `[Suggestion]` (optional). The review ends with one of three verdicts:

- **Passes** — objective achieved, all criteria met
- **Passes with minor suggestions** — objective achieved; suggestions noted
- **Needs revision** — blocking findings; objective not met

Both "Passes" and "Passes with minor suggestions" move the issue to Human Review automatically. "Needs revision" moves it to Revisions Needed.

The agent reviews up to **2 rounds**. After that it auto-escalates to Human Review regardless.

---

## Responding to Feedback

Whether the feedback is from the agent or the PI, the response format is the same: quote each finding, explain what you changed. The workflow afterward differs.

If the agent passes your work, the issue moves to Human Review automatically. Nothing for you to do.

When the verdict is "Needs revision", fix the issues and post a comment quoting each finding:

```
> [Blocking] The timeline is not clear end-to-end.

Fixed. Added a timeline table at the top of Section 1 showing
survey order and dependencies.

> [Blocking] Dependencies between surveys are only partially specified.

Fixed. Each survey section now states its prerequisites explicitly.
```

Don't just post "Updated the document." The reviewer needs to know which issues you addressed and how.

`[Suggestion]` items are always optional, whether from the agent or the PI. Skip them if you want.

**After agent feedback:** post your response and move the issue back to Agent Review — or post `/review` as a comment to trigger it without moving the issue.

**After substantive PI feedback:** if the PI gave you real revisions — not just a quick approval note — go back through agent review after fixing them. The agent stops reviewing after 2 rounds by default, so first post `/reset-reviews` to restart the counter, then move the issue back to Agent Review. This ensures updated work gets a fresh agent check before the PI looks again.

### Improving the agent

**If the feedback seems off:** post `/flag-feedback` as a comment, followed by a short explanation of what was wrong:

```
/flag-feedback The agent flagged the timeline as blocking but the timeline
was already in the document — it just used a different format than expected.
```

This flags the issue for the PI to review later and skips ahead to Human Review. The PI uses these flags to improve the agent's review instructions. The more specific you are about what went wrong, the faster the agent gets better.

If you just want to skip agent review without flagging a problem, use `/escalate` instead.

### Commands

Post any of these as a comment on the issue:

| Command | What it does |
|---------|-------------|
| `/review` | Re-trigger the agent review |
| `/reset-reviews` | Reset the 2-round review counter — use after substantive PI feedback |
| `/fix` | Auto-implement the agent's code feedback in a new commit (code tasks only) |
| `/escalate` | Skip agent review and go straight to Human Review |
| `/flag-feedback` | Flag bad agent feedback for PI review, then skip to Human Review |

---

## Linear in Slack

The best way to create an issue from Slack is to mention **`@Linear`** in any channel and describe the task in plain English:

```
@Linear read the last few messages for context. Create an issue for
cleaning the EZ shapefile and assign to Evely. Add Reviewer: ntsivanidis
as a label. Put it in the Lagos project.
```

The agent reads the conversation context and creates the issue. Always open it in Linear afterward to verify the fields are correct.

### Other ways to create issues from Slack

- **Message actions:** hover over any Slack message → click **⋯ More actions** → **Create Linear issue**. The message pre-fills the description.
- **Slash command:** type `/linear` to create an issue, or `/linear search` to find one.

### Notifications

Turn on Slack notifications — you'll catch review feedback faster than email. Set this up in Linear under **Settings → Notifications → Slack**. You can also subscribe a Slack channel to a project's updates to keep the whole team aware.

---

## Keyboard Shortcuts

You don't need these on day one. Come back once you're comfortable with the basics.

Press **`?`** at any time to open Linear's full shortcut reference. These are the ones worth learning first:

**Navigation**

| Shortcut | Action |
|----------|--------|
| `⌘K` | Command menu — search anything, jump anywhere |
| `G` then `I` | Go to Inbox |
| `G` then `M` | Go to My Issues |
| `G` then `P` | Go to Projects |
| `J` / `K` | Move down / up in any list |

**Issues**

| Shortcut | Action |
|----------|--------|
| `C` | Create new issue |
| `S` | Change status on selected issue |
| `A` | Assign issue |
| `L` | Add/change labels |
| `P` | Set priority |
| `Space` | Peek at issue without opening it |

**Inbox**

| Shortcut | Action |
|----------|--------|
| `E` | Mark notification as done |
| `U` | Mark as read |
| `Backspace` | Delete notification |

---

## FAQ

**The agent asked for a summary — where do I post it?**
As a comment on the issue. Use the template in the **Before Submitting for Review** section.

**I submitted for review but nothing happened.**
Check that the Reviewer label is set on the issue. The agent only reviews issues that have one.

**The agent keeps saying "Needs revision" — what do I do?**
After 2 rounds it auto-escalates to Human Review. If you think the feedback is wrong, post `/flag-feedback` with an explanation of what's off, or `/escalate` to skip it. The PI can post `/reset-reviews` after giving you guidance if they want the agent to try again.

**How do I share a Google Doc with the agent?**
Share the doc (or its parent Drive folder) with the service account email shown in the agent's error message. It looks like `name@project-id.iam.gserviceaccount.com`. Grant Viewer access. Sharing the parent folder covers all docs in it.

**My deliverable is a commit, not a PR — is that okay?**
Yes. Use the full commit URL from GitHub (the URL ending in the commit hash, e.g. `.../commit/abc1234...`). Don't link to a branch or file tree.

**What's the difference between `/fix` and fixing it myself?**
`/fix` tells the agent to implement its own feedback automatically in a new commit. It works well for clear, bounded fixes (wrong file path, missing column). For anything requiring judgment — restructuring a document, changing an analytical approach — fix it yourself.
