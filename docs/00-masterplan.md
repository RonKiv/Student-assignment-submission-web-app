# 00 · Masterplan: School Assignment Submission System

> **Version 1 · 8 Nov 2026 · Owner: Ronnie**
> This file is the single source of truth for *what* we're building and *when*. Only Ronnie edits it. Anyone can propose a change by opening a GitHub issue with the `plan-change` template or by messaging Ronnie.

## 1. The idea
A school-wide web app, like Google Classroom or Microsoft Teams but for the whole of KDU. **Teachers** post assignments with deadlines, **students** upload their work before the deadline, and an **admin** manages courses and accounts.

This is our final project for Web Application Development. It's graded on a **live demo**, a **written report** and a **presentation (PPT)**.

Working name: **[TBD]** (see Open items).

## 2. Team
| Person | Role | OS |
|---|---|---|
| Ronnie | Project lead and builder. Owns this plan, the task board, priorities, the core files (see 03-team-workflow), and has final say on scope and design. | macOS |
| [Friend] | Builder. Picks tasks freely from the board and ships them. | Windows |

We both use Claude. Each of us has a personal Claude Project that syncs the `docs/` folder from our GitHub repo, so both of us work from the same plan.

## 3. Users and what they can do
| Role | Can do | Main pages |
|---|---|---|
| **Student** | See their courses, see assignments and deadlines, upload a submission, see grade and feedback, read announcements | Dashboard, Course, Assignment (submit), My grades |
| **Teacher** | See the courses they teach, create assignments, see who submitted (on time or late), download files, grade and give feedback, post announcements | Dashboard, Course, New assignment, Submissions, Grade |
| **Admin** | Manage student and teacher accounts, create courses, assign teachers, enrol students | Admin dashboard, Users, Courses |

## 4. Scope: three tiers
Every feature sits in exactly one tier. When time runs short, we cut from the bottom tier first.

### Tier A: must really work (real backend)
These features use real logins and real saved data (Supabase).
- **A1 Login with roles.** Users log in with email and password. Students, teachers and the admin each land on their own dashboard, and a user can't open another role's pages.
- **A2 Teacher posts an assignment.** Title, instructions, due date and time, and points are saved to the database, and the assignment appears for enrolled students.
- **A3 Student submits.** The student opens an assignment and uploads a file. The system records the time and marks the submission *on time* or *late*.
- **A4 Teacher sees submissions.** A list of who has and hasn't submitted for an assignment, with download links. Without this, A2 and A3 can't be shown in the demo.

### Tier B: looks real (complete HTML/CSS, sample data, nothing is saved)
These pages are fully designed and clickable, filled with realistic sample data, so the demo can show the whole system.
- Grading and feedback (the teacher grades; the student sees the grade and comments)
- Grade dashboard (an overview of a student's grades; class statistics for the teacher)
- Announcements and comments
- Admin panel (users, courses, assigning teachers)

### Tier C: stretch goals (only if Tier A is done by 29 Nov)
In this order:
1. Grading and feedback saved for real
2. Announcements saved for real
3. The admin creates courses and enrols students for real
4. Comments

### Out of scope
Calendar and reminders, email notifications, plagiarism checking, a Korean or bilingual interface, a mobile app, real KDU single sign-on, and chat or messaging.

## 5. Look and feel
A mix of **Google Classroom** and a **modern dashboard**: a left sidebar for navigation (like Teams or Notion), with clean, card-based content and plenty of white space (like Classroom). The interface is in English only. Exact colours, fonts and components get decided in the design system task (D-01) and stored in `css/base.css` as CSS variables.

## 6. Tech summary (details in 01-tech-architecture)
HTML, CSS and plain JavaScript · **Supabase** for logins, database and file storage · **GitHub** for code and tasks · **GitHub Pages** for the live site · VS Code with Live Server on both laptops.

There are no frameworks, no npm and no build step. That keeps the project close to what the course teaches and makes it run the same on Mac and Windows.

## 7. Timeline (4 weeks)
The due date is assumed to be **about 7 Dec 2026** (to be confirmed, see Open items). Each stage ends with a **gate**: a milestone we check before moving on.

| Week | Dates | Focus | Gate (must be true by the end) |
|---|---|---|---|
| 1 | Mon 9 – Wed 11 Nov | Align and set up | **M0:** the repo is live and both of us can push; [Friend]'s existing work has been reviewed; the Supabase project exists; the board is filled |
| 1 | Wed 11 – Sun 15 Nov | Design system and first pages | **M1:** the design system and page template are done; login, student dashboard, course and assignment pages are built (static) |
| 2 | 16 – 22 Nov | Every remaining page (static), plus backend setup | **M2 (safety net):** the *whole* site is clickable with sample data and live on GitHub Pages. Database tables, file storage and demo accounts exist |
| 3 | 23 – 29 Nov | Tier A backend | **M3:** on the live site, with real logins, a teacher posts an assignment, a student uploads a file, and the teacher sees it |
| 4 | 30 Nov – 6 Dec | Tier C (if there's time), polish, testing, report, PPT, rehearsal | **M4:** everything is ready to submit, and the demo has been rehearsed on both laptops |

**Rules**
- M2 and Tier A are protected. If a gate slips, cut Tier C first, then Tier B polish.
- JavaScript is new to both of us, so we learn it *alongside* the page work in weeks 1–2 (about 2 hours each), not before starting.
- Take screenshots at every gate. They become material for the report and the PPT.

## 8. Deliverables
| Deliverable | What it needs | When |
|---|---|---|
| Live demo | Deployed site, demo accounts (1 admin, 2 teachers, 4 students), sample courses, a demo script | Script drafted in week 3, rehearsed in week 4 |
| Written report | Problem, users, features, design decisions, architecture, data model, screenshots, challenges, future work | Outlined in week 2, written in week 4 |
| Presentation (PPT) | The problem, our solution, the live demo, how it works, what we learned | Week 4 |

The **Decision log** below and the rest of `docs/` are the raw material for the report.

## 9. Decision log
| Date | Decision | Why |
|---|---|---|
| 8 Nov | Real backend only for login, posting and submitting (Tier A); everything else only looks real | Neither of us has written JavaScript, and we have 4 weeks at 5–10 hours a week each |
| 8 Nov | Supabase instead of Firebase | Supabase covers logins, database and file storage in one service, and its free plan includes 1 GB of file storage with no card required. Firebase file storage now requires the pay-as-you-go plan |
| 8 Nov | No frameworks or build tools | Stays close to the course and works the same on Mac and Windows |
| 8 Nov | English only | Keeps the scope manageable |
| 8 Nov | Classroom-style cards inside a sidebar dashboard | The chosen look and feel |
| 8 Nov | Ronnie owns the plan; [Friend] builds freely, task by task; check-ins are async | Our working agreement (see 03-team-workflow) |

## 10. Risks
| Risk | What we do about it |
|---|---|
| The backend takes longer than planned (no JavaScript experience) | Build the frontend first. The M2 safety net means the demo works even if the backend is late. The backend is limited to Tier A, and Claude helps write *and explain* the JavaScript |
| We can't explain our own code in the demo Q&A | Rule: no code is merged unless its author can explain every line |
| HTML/CSS quality drops because the backend takes up time | The course grades HTML/CSS, so weeks 1–2 are pure HTML/CSS, and Tier B pages get the same polish as Tier A pages |
| [Friend]'s existing work doesn't fit the plan | It's reviewed in task S-02, and each piece is kept, adapted or parked |
| The free Supabase project pauses after 7 days with no activity | Use it every week, and check it's awake 2 days before the demo. Un-pausing keeps all the data |
| Differences between Mac and Windows break something | Follow 02-conventions, and test on both laptops at every gate |
| Merge conflicts, or the design drifting between pages | The core files rule and the shared CSS components (see 03-team-workflow) |
| Working async means losing track of who's doing what | The GitHub board is the record of truth, and Ronnie posts a 3-line update every week |
| The professor doesn't allow or credit a backend | Check the assignment brief (see Open items) |

## 11. Open items (Ronnie to fill in)
- [ ] Assignment brief or rubric, and the exact due date
- [ ] Confirm that JavaScript and Supabase are allowed
- [ ] What [Friend] has already built (files, screenshots, Figma) → task S-02
- [ ] [Friend]'s name and GitHub username
- [ ] Project name
