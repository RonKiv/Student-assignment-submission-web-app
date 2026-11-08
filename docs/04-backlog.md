# 04 · Backlog

> Every task in the project. Each one becomes a GitHub Issue (title: `[ID] Task name`). Ronnie moves tasks into **Ready** each week; whoever is free takes the top one.
> **Owner** is blank when either of us can do it. ★ = touches a core file, so Ronnie merges it.

## Stage 1: Set up and align (Mon 9 – Wed 11 Nov) → Gate M0
| ID | Task | Owner | Done when… |
|---|---|---|---|
| S-01 | Create the GitHub repo, add the starter kit, invite [Friend], create the Projects board, and turn this backlog into issues | Ronnie | [Friend] can push a branch; the board has its columns and issues |
| S-02 | Review [Friend]'s existing work: keep, adapt or park | Ronnie + [Friend] | Every piece is labelled; kept pieces have an issue to adapt them |
| S-03 | Install the tools on both laptops: VS Code, the Live Server and EditorConfig extensions, GitHub Desktop; clone the repo | Both | Both of us can open the repo in VS Code and run a page in Live Server |
| S-04 | Create the Supabase project and invite [Friend] | Ronnie | We can both open the dashboard; the project URL and publishable key are noted in a safe place |
| S-05 | Set up personal Claude Projects synced to the repo (03-team-workflow § 7) | Both | Each Project has the instructions and the synced `docs/` |
| S-06 | Turn on GitHub Pages | Ronnie | A placeholder page is reachable at the github.io address |

## Stage 2: Design system (Wed 11 – Sun 15 Nov) → Gate M1
| ID | Task | Owner | Done when… |
|---|---|---|---|
| D-01 ★ | Design system: colours, font, spacing, radius and shadow variables in `base.css`; buttons, cards, forms, tables, badges and alerts in `components.css`; a `styleguide.html` that shows them all | Ronnie | Every token in 02-conventions § 6 has a value; the styleguide looks right on Mac and Windows |
| D-02 ★ | Page template and `layout.css`: a sidebar (student, teacher and admin link sets), a top bar (name, logout), the main content area | | A blank page made from the template looks finished; the sidebar collapses on a phone-width screen |

## Stage 3: Static pages with sample data (weeks 1–2) → M1 and Gate M2
Done when, for every page: it's built from the template, uses only shared components and variables, is filled with realistic sample data, all its links work, and it holds up at 375 px.

| ID | Page | Tier | Extra checks |
|---|---|---|---|
| P-01 | Login (`index.html`) | A | Error message styles for a wrong password |
| P-02 | Student dashboard | A | Course cards and a "due soon" list |
| P-03 | Student course page | A | Assignment list and an announcements area |
| P-04 | Student assignment page | A | Upload form, plus all four states: not submitted / submitted / late / graded |
| P-05 | Student grades | B | Grades table and a simple summary |
| P-06 | Teacher dashboard | A | Courses taught and a "needs grading" list |
| P-07 | Teacher course page | A | Assignment list and a "new assignment" button |
| P-08 | New assignment form | A | All fields with labels, and validation styles |
| P-09 | Submissions list | A | On time / late / missing badges and download links |
| P-10 | Grade submission page | B | Grade input and a feedback box |
| P-11 | Admin dashboard | B | Counts and shortcuts |
| P-12 | Admin users | B | Users table and an add/edit form |
| P-13 | Admin courses | B | Courses table, assign teacher, enrol students |
| P-14 | Announcements and comments UI on the course pages | B | Post form and a list |
| P-15 | Link check across every page, then deploy | Ronnie | **Gate M2:** the whole site is clickable on the live URL |

## Stage 4: Learn JavaScript (alongside weeks 1–2, about 1 hour each)
| ID | Task | Owner | Done when… |
|---|---|---|---|
| J-01 | DOM and events: change the page, react to clicks and form submissions | Both | Each of us builds a tiny demo and can explain it |
| J-02 | `async` / `await` and the supabase-js basics | Both | Each of us reads one row from Supabase into the page |

## Stage 5: Backend setup (week 2)
| ID | Task | Owner | Done when… |
|---|---|---|---|
| K-01 ★ | Create the tables from 01-tech-architecture § 5, with RLS on; save the SQL in `supabase/schema.sql` | | The tables exist; RLS is enabled on every table |
| K-02 ★ | Create the `submissions` storage bucket and its access rules | | A student can upload only into their own folder; the course's teacher can read it |
| K-03 | Demo accounts and sample data: 1 admin, 2 teachers, 4 students, 3 courses, enrolments, a few assignments; save as `supabase/seed.sql` | | We can log in as every demo user in the dashboard |
| K-04 ★ | `js/supabase-client.js`: the connection using the publishable key | | A test page reads data without errors |

## Stage 6: Tier A backend (week 3) → Gate M3
| ID | Task | Covers | Done when… |
|---|---|---|---|
| A-01 ★ | Login, logout, and redirecting by role in `auth.js` | A1 | Each demo user lands on the right dashboard; logout works |
| A-02 | `requireRole()` on every protected page | A1 | A student who types a teacher page URL is sent back to their own dashboard |
| A-03 | Dashboards load real courses (enrolled courses for students, taught courses for teachers) | A1 | Course cards come from the database |
| A-04 | The teacher's new-assignment form saves to the database | A2 | A new assignment appears in the database and on the course page |
| A-05 | Course pages list real assignments | A2 | Students see only the assignments for their courses |
| A-06 | A student uploads a file: it's stored, a submission row is created, and on time / late is recorded | A3 | The file is in Storage; `is_late` is correct around the deadline |
| A-07 | The assignment page shows the real submission status | A3 | The status updates after an upload |
| A-08 | The teacher's submissions list shows real data with download links | A4 | The teacher sees who submitted and can download the files |
| A-09 | End-to-end test on the live site, on both laptops | — | **Gate M3:** the full flow works on Mac and Windows |

## Stage 7: Stretch (week 4, only if M3 passed by 29 Nov)
| ID | Task | Done when… |
|---|---|---|
| C-01 | Grading and feedback saved; the student sees the grade | The grade appears on the student's page after the teacher saves it |
| C-02 | Announcements saved for real | A posted announcement appears for enrolled students |
| C-03 | The admin creates courses and enrols students for real | A new course appears for its teacher and students |
| C-04 | Comments saved for real | A comment thread persists after reloading the page |

## Stage 8: Finish (week 4) → Gate M4
| ID | Task | Owner | Done when… |
|---|---|---|---|
| R-01 | Polish pass: consistency, empty states, error messages | Both | Every page has been checked against the styleguide |
| R-02 | Cross-device test: Chrome and Safari on Mac, Chrome and Edge on Windows, phone width | Both | Bugs found are fixed or logged |
| R-03 | Demo script and a way to reset the demo data | Ronnie | The script runs in under 7 minutes |
| R-04 | Written report | Both, split by section | Draft reviewed by both of us |
| R-05 | Presentation (PPT) | Both | Slides finished; the demo is embedded or linked |
| R-06 | Rehearse the demo twice (once on each laptop); confirm Supabase is awake | Both | **Gate M4** |
