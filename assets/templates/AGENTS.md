<!-- TEMPLATE. Replace every <…>. Delete sections that don't apply. Keep it specific to this project. -->
# AGENTS.md — <project name>

Instructions for any AI coding agent and human developer working in this repository. Read fully before changing anything.

## 1. What we are building
<3–5 lines: what, for whom, the main parts (e.g. public site, admin, API)>.
Product requirements: [`docs/PRD.md`](docs/PRD.md). Build order and phase gates: [`docs/ROADMAP.md`](docs/ROADMAP.md).

## 2. Read before you code
| When you are… | Read |
|---|---|
| Starting any task | This file, then the current phase in `docs/ROADMAP.md` |
| <Touching structure or a new module> | `docs/ARCHITECTURE.md`, `docs/adr/` |
| <Adding or upgrading a dependency> | `docs/STACK.md` |
| <Building UI> | `docs/DESIGN-SYSTEM.md` |
| <Writing tests or finishing a task> | `docs/TESTING.md` |
| <Input, auth, files, secrets, personal data> | `docs/SECURITY.md` |

If a doc and the code disagree, stop and ask.

## 3. Stack (pinned, change only via ADR)
<one line, e.g. Node 24 · pnpm · TypeScript 6 · Astro 7 · PostgreSQL 18 · Vitest · Playwright>. Exact versions: `docs/STACK.md`.

## 4. Repository layout
```
<tree with one-line purpose per folder>
```
<Dependency direction rules, e.g. apps may import packages; packages never import apps.>

## 5. Commands
```bash
<install / dev / lint / typecheck / test / test:e2e / build / check>
```
<Mark "available after Phase 0" if not scaffolded yet.>

## 6. How to work
1. One phase at a time (current phase in ROADMAP). Don't start the next until its gate passes and the owner approves.
2. Plan first for anything touching more than two files.
3. Small vertical slices. Tests are part of the task.
4. Update docs and tick ROADMAP boxes in the same change.
5. Ask before: adding dependencies, changing the stack or data model, deleting data or files, changing public URLs, touching production.

## 7. Definition of done
- [ ] `<check command>` passes (lint, typecheck, tests)
- [ ] New logic has tests; bugs get a regression test first
- [ ] <UI works in each language/direction and at mobile + desktop widths>
- [ ] No hard-coded secrets, colors or UI strings
- [ ] Access control defined and tested for new resources
- [ ] Docs and ROADMAP updated

## 8. Non-negotiable rules
**Security:** <validate input at the boundary with shared schemas; default-deny access; secrets only via validated env; anti-spam on public forms>.
**Code quality:** <strict types, no any, file size limits, business logic in pure tested modules, never edit generated files>.
**UI:** <design tokens only; logical CSS properties for RTL; all copy through i18n>.
**Language:** code, commits and technical docs in English. UI in <languages>. Owner docs (PRD, ROADMAP, OPEN-QUESTIONS) in <owner's language>.

## 9. Git
Branches `phase-<n>/<topic>` · Conventional Commits · PR template · CI green before merge · never commit to `main` directly.

## 10. Never do
- Commit `.env` files, real customer data or credentials
- Disable lint rules, tests or type checks to pass
- Add a dependency without justification
- Change public URLs without redirects
- Run destructive DB commands on staging or production
- <project-specific: e.g. add server credentials to GitHub (deploys are pull-only)>
