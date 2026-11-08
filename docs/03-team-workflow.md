# 03 · Team Workflow

> How Ronnie and [Friend] build one project together, mostly asynchronously, with Ronnie setting the direction.

## 1. The working agreement
**Ronnie owns the plan. [Friend] builds freely within it.**

| Ronnie decides | [Friend] decides |
|---|---|
| What's in scope (the tiers) and the timeline | Which task to pick next from "Ready" |
| What goes on the board, and in what order | How to build a task, within the conventions |
| The design system and the core files | When their task is done (using the Definition of Done) |
| Any change to `docs/` | |
| Final say if we disagree | |

[Friend] doesn't need sign-off for each task. Ronnie keeps control through **the plan, the board and the core files**, not by approving every line.

## 2. Tools
| Tool | Used for | Who |
|---|---|---|
| GitHub repository | All code and `docs/` | Ronnie (owner), [Friend] (collaborator) |
| GitHub Projects board | The task list we both work from | Ronnie maintains it |
| GitHub Desktop | Committing, pushing and pulling without the terminal | Both |
| VS Code with Live Server | Editing and previewing | Both |
| Supabase | Backend | Ronnie (owner), [Friend] (invited) |
| KakaoTalk | Quick questions and the weekly update | Both |
| Claude | Each person's own Claude Project, synced to the repo's `docs/` | Both |

## 3. The board
The columns are **Backlog → Ready → In progress → In review → Done**.
- **Backlog:** everything in 04-backlog.
- **Ready:** what Ronnie wants done *this week*, in priority order. Either of us takes the top card.
- **In progress:** assign yourself when you start. Each person has at most **2** tasks in progress.
- **In review:** a pull request is open.
- **Done:** merged into `main`.

Every task is a GitHub Issue that says what to build, which tier it belongs to, and its **"Done when…"** checks.

## 4. Life of a task
1. Take the top card in **Ready**, assign yourself, and move it to **In progress**.
2. In GitHub Desktop, pull `main` and create a branch named `task/<number>-<short-name>`.
3. Open a fresh Claude chat in your Project for this task (see § 7) and build it.
4. Check your work against the **Definition of Done** (below).
5. Push, open a pull request that includes `Closes #<number>`, and move the card to **In review**.
6. Merging:
   - For a normal task, the author merges their own pull request once the checklist is ticked. Ronnie gets a notification and looks it over when he can. Anything that needs fixing becomes a new issue rather than blocking the merge.
   - For a task that touches a **core file**, Ronnie reviews and merges.
7. Delete the branch. The card moves to **Done**.

## 5. Definition of Done (copied into every pull request)
- [ ] Meets every "Done when…" check in the issue
- [ ] Follows 02-conventions (lowercase-hyphen names, relative paths, CSS variables, shared components)
- [ ] Works in Live Server with no errors in the browser console
- [ ] Doesn't break at 375 px width
- [ ] I can explain every line I'm committing
- [ ] Screenshot attached to the pull request (material for the report)

## 6. Core files
Every page depends on these files, so a change to one affects the whole site:
`css/base.css`, `css/layout.css`, `css/components.css`, `js/supabase-client.js`, `js/auth.js`, `supabase/schema.sql`, the page template, everything in `docs/`, and `CLAUDE.md`.
- To change one, first open an issue (or message Ronnie), then open a pull request for Ronnie to merge.
- This prevents the two most common problems when two people build one site: merge conflicts, and the site gradually looking like two different sites.

## 7. Claude setup (both of us)
In Claude, sharing a Project only works on Team or Enterprise plans. So each of us keeps a **personal** Claude Project, and they stay aligned because both read the **same files from the repo**:
1. Create a Claude Project (for example "Assignment System").
2. Paste the shared instructions from `docs/claude-project-instructions.md` into the Project's instructions.
3. In Project knowledge, choose **+ → GitHub**, pick our repo, and select `docs/` and `CLAUDE.md`. Add code folders later when they're useful.
4. Before starting a task, press **Sync** so Claude has the latest plan and code.
5. **One task per chat.** Name the chat after the issue, for example `#14 Student dashboard`.

Ronnie also keeps a **Masterplan chat**, the only place plan changes are made. When the plan changes, Ronnie updates `docs/`, commits the change, and posts one line in KakaoTalk ("Plan updated: …"). Then we both press Sync.

If you use Claude Code, it reads `CLAUDE.md` in the repo root automatically.

## 8. Communication (async)
- **Default:** async, on KakaoTalk or in GitHub comments. Ask for help if you've been stuck for more than about 30 minutes.
- **Kickoff (once, about 30 minutes, this week):** walk through the masterplan, review what [Friend] has already built, set up GitHub and Supabase access together, and agree on the first week's Ready column.
- **Weekly update (Ronnie, Sunday night, 3 lines in KakaoTalk):** what got done, what's Ready next week, and any plan change.
- **Gate check (end of each stage):** Ronnie checks the gate in 00-masterplan and posts pass or fail. A failed gate means a short call to re-plan.

## 9. Bringing in [Friend]'s existing work (task S-02)
1. [Friend] shares everything built so far (files, screenshots, Figma links).
2. Ronnie reviews it in a Claude chat against this plan and marks each piece **keep**, **adapt** or **park**.
3. [Friend] commits the kept work to the repo on a branch, adapts it to the conventions, and merges it.
4. Parked ideas go into the Backlog, so nothing gets lost.

## 10. Suggested chats in Ronnie's Claude Project
| Chat | Purpose |
|---|---|
| Masterplan | Plan changes, priorities, re-planning |
| Setup: GitHub and Supabase | Step-by-step setup (S-01, S-03, S-04, S-06) |
| Review: [Friend]'s work | Task S-02 |
| Design system | D-01, D-02 |
| One chat per page or task | Named `#<issue> <name>` |
| Learn JS | The concepts in 01-tech-architecture § 10, taught from scratch |
| Backend | Tier A tasks (K and A tasks) |
| Report | The written report |
| Presentation | The PPT and the demo script |
