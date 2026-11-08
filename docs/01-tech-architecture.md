# 01 · Tech and Architecture

> How the system is built. Changing the stack is a plan change, so it needs Ronnie's approval.

## 1. The stack and why
| Layer | Choice | Why this one |
|---|---|---|
| Pages | HTML5 | It's what the course teaches |
| Styling | Plain CSS with CSS variables | It's the course focus, and the variables keep both of us on one design |
| Behaviour | Plain JavaScript (no frameworks) | The smallest tool that can talk to a backend, with nothing to install |
| Backend | Supabase (cloud): Auth, a Postgres database, Storage | Logins, data and file uploads in one service. It runs in the cloud, so it's the same on Mac and Windows. Free plan, no card needed |
| Hosting | GitHub Pages | Free static hosting directly from the repo |
| Code and tasks | GitHub (repo, Issues, Projects board) | One place for code, tasks and reviews |
| Editor | VS Code with the Live Server extension | The same tool on both OSes |
| Git client | GitHub Desktop (the terminal is optional) | No command line needed on either OS |

Supabase is loaded with a single `<script>` tag from a CDN. There's no npm and no build step.

**Free-plan limits that matter:** 1 GB of file storage, a 500 MB database, and 2 projects. The project also **pauses after 7 days with no activity**. The data is kept, and you can un-pause it from the dashboard.

## 2. How it fits together
```
 Browser (student / teacher / admin)
        │  loads HTML/CSS/JS from
        ▼
 GitHub Pages  ── static files from our repo (main branch)
        │  JS calls (supabase-js)
        ▼
 Supabase
   ├─ Auth      → who you are (email + password)
   ├─ Database  → profiles, courses, assignments, submissions …
   └─ Storage   → uploaded files (bucket: submissions)
```
We don't run a server of our own. The browser talks to Supabase directly, and Supabase's **Row Level Security (RLS)** rules decide what each logged-in user can read or write.

## 3. Folder structure
```
<repo>/
├── index.html              ← login page (everyone starts here)
├── styleguide.html         ← shows every component (task D-01)
├── student/
│   ├── dashboard.html
│   ├── course.html         ← ?id=<course id>
│   ├── assignment.html     ← ?id=<assignment id>  (view + submit)
│   └── grades.html
├── teacher/
│   ├── dashboard.html
│   ├── course.html
│   ├── new-assignment.html
│   ├── submissions.html    ← ?assignment=<id>
│   └── grade.html          ← ?submission=<id>
├── admin/
│   ├── dashboard.html
│   ├── users.html
│   └── courses.html
├── css/
│   ├── base.css            ← CORE: reset, CSS variables (colours, fonts, spacing), typography
│   ├── layout.css          ← CORE: sidebar, top bar, page grid
│   ├── components.css      ← CORE: buttons, cards, forms, tables, badges, alerts
│   └── pages/              ← page-specific styles, only if really needed
├── js/
│   ├── supabase-client.js  ← CORE: creates the Supabase connection
│   ├── auth.js             ← CORE: login, logout, requireRole()
│   ├── assignments.js
│   ├── submissions.js
│   └── ui.js               ← small shared helpers (format dates, show messages)
├── assets/
│   ├── images/
│   └── icons/
├── supabase/
│   ├── schema.sql          ← tables + RLS rules (task K-01)
│   └── seed.sql            ← demo data (task K-03)
├── docs/                   ← the plan (00–04). Only Ronnie edits these.
├── CLAUDE.md               ← instructions Claude reads first
└── README.md
```
Every page uses the **CORE** files. See 03-team-workflow for how changes to them work.

## 4. Pages (sitemap)
| Page | Role | Tier | Notes |
|---|---|---|---|
| `index.html` Login | all | A | Sends each user to the right dashboard after login |
| Student dashboard | student | A | Course cards and a "due soon" list |
| Student course | student | A | Course info, assignment list, announcements (B) |
| Student assignment | student | A | Instructions, due date, upload, submission status |
| Student grades | student | B | Grades table and simple statistics |
| Teacher dashboard | teacher | A | Courses taught and submissions needing attention |
| Teacher course | teacher | A | Assignment list, announcements (B) |
| New assignment | teacher | A | Form that saves to the database |
| Submissions | teacher | A | Who submitted, on time or late, download links |
| Grade submission | teacher | B → C | Grade and feedback form |
| Admin dashboard | admin | B | Counts and shortcuts |
| Admin users | admin | B | Users table, add and edit forms (look real only) |
| Admin courses | admin | B → C | Courses table, assigning teachers, enrolling students |

Every logged-in page shares a sidebar (with role-specific links) and a top bar (user name and logout).

## 5. Data model (Supabase / Postgres)
```
profiles      (id = auth user id, full_name, role: student|teacher|admin, department, created_at)
courses       (id, code, title, semester, teacher_id → profiles)
enrollments   (course_id → courses, student_id → profiles)          -- who takes which course
assignments   (id, course_id → courses, title, instructions, due_at, max_points, created_at)
submissions   (id, assignment_id → assignments, student_id → profiles,
               file_path, submitted_at, is_late,
               grade, feedback, graded_at)                            -- grade/feedback are used in Tier C
announcements (id, course_id → courses, author_id → profiles, body, created_at)   -- Tier C
```
- **Storage bucket:** `submissions`, with file path `<assignment_id>/<student_id>/<file name>`.
- `is_late` is set when the student submits: it's true when `submitted_at` is later than `due_at`.
- Tier B pages use sample data written into the HTML, so they don't need tables yet.

## 6. Login and roles
- Users log in with email and password (Supabase Auth).
- Each user's role is stored in `profiles.role`.
- At the top of every protected page, `auth.js` runs `requireRole('teacher')` (or student/admin). If there's no session, the user goes back to the login page. If the role is wrong, they go back to their own dashboard.
- That check is only a convenience. **The real protection is RLS** in the database. For example, a student can only read their own submissions, and a teacher can only read submissions for the courses they teach.
- Demo accounts (1 admin, 2 teachers, 4 students) are created from the Supabase dashboard, not from the site. Creating accounts *for other people* from the browser would need a secret key, and that key must never be in front-end code. That's why the admin "add user" form is Tier B.

## 7. Security rules (non-negotiable)
- Only the Supabase **publishable key** (older projects call it the *anon* key) goes in `js/supabase-client.js`. It's designed to be public; RLS is what protects the data.
- The **secret (service_role) key never goes in the repo, a chat or a screenshot.**
- RLS is switched on for every table before any real data goes in.
- Uploads: PDF, DOCX, PPTX, ZIP and images are allowed, up to about 10 MB.

## 8. Local development
1. Clone the repo with GitHub Desktop.
2. Open the folder in VS Code.
3. Right-click `index.html` → **Open with Live Server**. Always use Live Server. Double-clicking a file opens it as `file://`, where logins and some scripts don't work properly.
4. Edit and save; the browser reloads on its own.

## 9. Deployment
GitHub Pages serves the `main` branch. Anything on `main` goes live within a minute or two, so only finished, working code goes into `main`.

On a free GitHub account, GitHub Pages needs the repo to be **public**. To keep the repo private, Ronnie can claim the free GitHub Student Developer Pack, which includes GitHub Pro and allows Pages from private repos.

## 10. The only JavaScript we need to learn
Learn these in order, as the tasks need them. Claude can teach each one from scratch.
1. Selecting elements and changing the page (the DOM)
2. Responding to clicks and form submissions (events)
3. Waiting for the network with `async` / `await`
4. Supabase calls: sign in, select, insert, upload a file
5. Building HTML from data (looping over results to make cards or table rows)
