# 02 · Conventions

> Rules that make two people's code read like one person wrote it, and make sure it works on both Mac and Windows.

## 1. Mac and Windows rules (most important)
| Rule | Why |
|---|---|
| File and folder names are **lowercase, with words joined by hyphens**: `new-assignment.html`, never `New Assignment.html` or `newAssignment.html` | Mac and Windows ignore capital letters in file names, but GitHub Pages doesn't. A wrong capital letter works on your laptop and breaks only on the live site |
| Links and paths are **relative, with forward slashes**: `../css/base.css`, never `C:\...` or `/Users/...` | Backslashes and absolute paths only work on one machine |
| Use the shared **web font** loaded in `base.css`, never a system font name | Mac (SF Pro) and Windows (Segoe UI) have different built-in fonts, so the site would look different on each |
| Keep the repo's `.gitattributes` and `.editorconfig` files | Windows and Mac end lines differently (CRLF vs LF). Without these files, every line can show up as "changed" |
| Never commit `.DS_Store` (Mac) or `Thumbs.db` (Windows) | `.gitignore` already blocks them |
| Always open pages through **Live Server** | Pages then behave the same on both OSes and on the live site |
| Test in Chrome **and** in Safari (Mac) or Edge (Windows) at every gate | Catches browser differences early |

## 2. HTML
- Every page starts from the shared page template (made in task D-02), so the sidebar, top bar and `<head>` are identical everywhere.
- Use semantic tags: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`, and `<button>` for buttons (not clickable `<div>`s).
- Every `<img>` has `alt` text, and every form input has a `<label>`.
- Indent with 2 spaces and put attribute values in double quotes.
- Each page has one `<h1>`.

## 3. CSS
- **Use the variables** from `base.css` for every colour, font size, spacing value, radius and shadow. Write `color: var(--color-text);`, never `color: #333;`.
- **Use the shared components** from `components.css` (`.btn`, `.card`, `.form-field`, `.table`, `.badge` and so on) before writing new styles. If a new component is needed, add it to `components.css`. That's a core file, so see 03-team-workflow first.
- Class names are lowercase and hyphenated, and describe *what something is*, not how it looks: `.assignment-card`, not `.blue-box`. Variants use `--`: `.btn--primary`, `.badge--late`.
- No inline `style=""` and no `!important`, except for a genuine emergency fix with a comment explaining it.
- Use Flexbox and Grid for layout. Pages must not break at a width of 375 px (phone size).
- Page-specific CSS goes in `css/pages/<page-name>.css`, and only when it can't be a shared component.

## 4. JavaScript
- Plain JavaScript, with no libraries except supabase-js.
- Use `const` by default and `let` when the value changes. Never use `var`.
- Variables and functions are named in `camelCase` (`loadAssignments`); file names are lowercase and hyphenated.
- Each function does one job and has a short comment above it explaining *why* it exists.
- Every Supabase call checks for an error and shows a friendly message (via `ui.js`). Nothing fails silently.
- Load scripts at the end of `<body>`, or use `defer`.
- **You must be able to explain every line you commit.** If Claude wrote something you can't explain, ask Claude to explain it before you commit.

## 5. Git
- Never work directly on `main`. Use one branch per task, named `task/<issue-number>-<short-name>`, for example `task/14-student-dashboard`.
- Commit messages are in the present tense and say what changed: `Add upload form to assignment page`.
- Make small commits, often. Pull `main` before starting a new task.
- Link the issue in the pull request: `Closes #14`.

## 6. Design tokens (placeholders until task D-01)
These get decided in the design system task and written into `base.css`:
`--color-primary`, `--color-bg`, `--color-surface`, `--color-text`, `--color-muted`, `--color-border`, `--color-success`, `--color-warning`, `--color-danger`,
`--font-body`, `--font-size-*`, `--space-*`, `--radius`, `--shadow`, `--sidebar-width`.
