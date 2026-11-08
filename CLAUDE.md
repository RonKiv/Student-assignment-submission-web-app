# CLAUDE.md

This repo is a two-person student project: a school-wide assignment submission system (students, teachers, admin) built with HTML, CSS, plain JavaScript and Supabase, and hosted on GitHub Pages. Ronnie (project lead) is on macOS; [Friend] is on Windows.

## Read before doing anything
- `docs/00-masterplan.md`: scope tiers (A must really work / B looks real / C stretch), timeline, decisions
- `docs/01-tech-architecture.md`: stack, folder structure, pages, data model, security rules
- `docs/02-conventions.md`: coding rules and Mac/Windows rules
- `docs/03-team-workflow.md`: branches, pull requests, Definition of Done, core files
- `docs/04-backlog.md`: task IDs and their "Done when…" checks

## Rules
- No frameworks, no npm, no build tools. supabase-js is loaded from a CDN.
- File names are lowercase-hyphenated, paths are relative with forward slashes, and styles use the CSS variables and shared components.
- Never write the Supabase secret (service_role) key anywhere. Only the publishable key goes in `js/supabase-client.js`.
- Core files (`css/base.css`, `css/layout.css`, `css/components.css`, `js/supabase-client.js`, `js/auth.js`, `supabase/schema.sql`, the page template, `docs/`, this file): say so whenever a change touches one, because Ronnie merges those.
- Don't change `docs/` unless Ronnie asks. If a task would change scope, stack, timeline or structure, stop and flag it as a plan change.
- We're JavaScript beginners: keep code small, commented and explainable line by line.
