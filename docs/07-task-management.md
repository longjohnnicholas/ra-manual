# Task Management with Linear

Your work lives in Linear as an issue. Move your card when your status changes — that's how the PI tracks progress without having to ask.

---

## Getting into Linear

Linear has a desktop app (preferred — download at [linear.app/download](https://linear.app/download)) and a web app at [linear.app](https://linear.app). Use the desktop app if you can; it's faster and sends notifications. If you can't install it, the web app works fine.

The PI will invite you via email when you join the lab. Once you're in, you'll see your projects in the left sidebar — one team per research project (Lagos, Ethiopia, etc.). Click your team to open the board.

If you haven't received an invite, ask the PI to send one.

---

## The Board

The board is a set of columns. Each column is a **status**. Each card is an **issue** — one task, assigned to one person.

Move a card by clicking its status and selecting a new one from the dropdown, or drag it to a different column.

| Status | What it means | When to move here |
|--------|--------------|-------------------|
| **Backlog** | Queued, not yet started | Set by PI |
| **Assigned** | Yours to do | When the PI assigns it to you |
| **In Progress** | You're actively working on it | As soon as you start |
| **Agent Review** | You've finished — ready to submit | When your work is complete |
| **Revisions Needed** | The agent found issues | Moved automatically — fix and resubmit |
| **Human Review** | Agent approved, PI is reviewing | Moved automatically |
| **Done** | Work accepted | Moved by PI |

Move the card when your status changes. If your card sits in "Assigned" while you're two days in, the PI has no visibility.

---

## The Review Timeline

To submit your work, change the card's status to **Agent Review** — click the status field and select it from the dropdown. An automated AI reviewer will then read your work and check it against the objective and acceptance criteria on the card. Here's the full flow:

```
In Progress
     |
     | (work complete — move card)
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

The agent reviews up to **2 rounds**. After that it escalates to Human Review — the PI decides. You can also skip the agent at any point with `/escalate`.

---

## Before Submitting for Review

Three things before you move to Agent Review:

### 1. Fill in the card description

Open the card and make sure the description has these three sections:

- **`## Objective`** — one sentence: what should this work achieve?
- **`## Acceptance Criteria`** — bullets: what does "done" look like?
- **`## Deliverable Links`** — the URL to your GitHub PR, commit, or Google Doc

The PI usually writes the Objective and Acceptance Criteria when they create the task. Don't rewrite them — just add your Deliverable Link.

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

### 2. Add a Reviewer label

On the card, find the **Labels** field (in the right-hand properties panel) and add a label in the format `Reviewer: name` — for example, `Reviewer: ntsivanidis`. This tells the agent and the PI who is doing the human review. If the label doesn't exist yet, you can create it from the labels panel.

### 3. Post a Summary comment

Scroll to the bottom of the card and post a comment using this template:

```
**Summary** @reviewer

**Task Purpose:** What the task was about (1-2 sentences).

**Procedure:** What you did (up to 5 sentences).

**Output Location:** Where to find the output. Include the final commit URL.

**Additional Notes:** Anything else relevant.
```

The summary must include a GitHub commit or PR URL. The agent checks for this before it starts reviewing — if it's missing, it will ask for it.

---

## What the Agent Reviews

The agent reads what you linked: the diff of your code changes (GitHub PR or commit) or the full text of a Google Doc. It checks your work against the Objective and Acceptance Criteria and produces a structured review.

Findings are tagged either `[Blocking]` (must fix to pass) or `[Suggestion]` (optional). The review ends with one of three verdicts:

- **Passes** — objective achieved, all criteria met
- **Passes with minor suggestions** — objective achieved; suggestions noted
- **Needs revision** — blocking findings; objective not met

Passes → card moves to Human Review automatically. Needs revision → card moves to Revisions Needed.

---

## Responding to Feedback

The same approach applies whether the feedback is from the agent or from the PI.

Fix the issues, then post a comment **quoting each piece of feedback** with what you changed:

```
> [Blocking] The timeline is not clear end-to-end.

Fixed. Added a timeline table at the top of Section 1 showing
survey order and dependencies.

> [Blocking] Dependencies between surveys are only partially specified.

Fixed. Each survey section now states its prerequisites explicitly.
```

Don't just post "Updated the document." The reviewer needs to know which issues you addressed and how.

**After agent feedback:** post your response and move the card back to Agent Review — or post `/review` as a comment to trigger it without moving the card. `[Suggestion]` items are optional. Skip them if you want.

**After substantive human (PI) feedback:** if the PI gave you real revisions to make — not just a quick approval note — go back through agent review after fixing them. First post `/reset-reviews` to restart the 2-round counter, then move the card back to Agent Review. This ensures the updated work gets a fresh agent check before the PI looks again.

**If the feedback seems wrong:** post `/escalate` to skip to Human Review and leave a comment explaining why you think the feedback missed the mark. This helps the PI calibrate and improve the agent's instructions over time.

---

## Commands

Post any of these as a comment on the Linear issue:

| Command | What it does |
|---------|-------------|
| `/review` | Re-trigger the agent review |
| `/reset-reviews` | Reset the review counter — use this after the PI gives you detailed feedback and you want more AI review rounds |
| `/fix` | Auto-implement the agent's feedback in the code (code tasks only) |
| `/escalate` | Skip agent review and go straight to the PI |

---

## Keyboard Shortcuts

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
As a comment on the card. Use the template from Step 3 above.

**The agent keeps saying "Needs revision" — what do I do?**
After 2 rounds it auto-escalates to Human Review. If you think the feedback is wrong, post `/escalate` to skip it. The PI can post `/reset-reviews` after giving you guidance if they want the agent to try again.

**How do I share a Google Doc with the agent?**
Share the doc (or its parent Drive folder) with the service account email shown in the agent's error message. Grant Viewer access. Sharing the parent folder covers all docs in it.

**My deliverable is a commit, not a PR — is that okay?**
Yes. Use the full commit URL from GitHub (the URL ending in the commit hash, e.g. `.../commit/abc1234...`). Don't link to a branch or file tree.

**What's the difference between `/fix` and fixing it myself?**
`/fix` tells the agent to implement its own feedback automatically. It works well for clear, bounded fixes (wrong file path, missing column). For anything requiring judgment — restructuring a document, changing an analytical approach — fix it yourself.
