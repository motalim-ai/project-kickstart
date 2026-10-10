# The doc set: what each file is for and what it must contain

## Contents
1. Folder layout
2. Sizing and when to include each doc
3. Required content per doc
4. Quality bar and final checks

---

## 1. Folder layout

```
.
├── AGENTS.md                  # rules for any AI agent / developer (English)
├── CLAUDE.md                  # imports AGENTS.md + Claude Code specifics (English)
├── README.md                  # what this is, quick start, where docs live
├── .gitignore  .editorconfig  .nvmrc (or equivalent)
├── .github/pull_request_template.md     (M/L)
├── design/                    # only if brand assets or prototypes exist
│   ├── brand/                 # logo, colors, fonts (source files)
│   └── prototypes/            # approved mockups + README
└── docs/
    ├── README.md              # index of docs (owner's language)
    ├── PRD.md                 # what & why (owner's language)
    ├── ROADMAP.md             # phases + test gates (owner's language)
    ├── OPEN-QUESTIONS.md      # unknowns, assumptions (owner's language)
    ├── STACK.md  ARCHITECTURE.md  CODING-STANDARDS.md  TESTING.md  SECURITY.md   (M/L)
    ├── DATA-MODEL.md  DESIGN-SYSTEM.md  DEPLOYMENT.md  DEPLOY-RUNBOOK.md        (L, when relevant)
    ├── SEO.md  TRACKING.md                                                     (public sites)
    └── adr/0000-template.md, 0001-…md                                          (M/L)
```

## 2. Sizing

| Doc | S | M | L | Include when |
|---|---|---|---|---|
| AGENTS.md, CLAUDE.md, README.md | ✓ | ✓ | ✓ | always |
| PRD.md | short | ✓ | ✓ | always (S: one page) |
| ROADMAP.md | 2–3 phases | ✓ | ✓ | always |
| OPEN-QUESTIONS.md | if any | ✓ | ✓ | any unknowns exist |
| STACK.md | in AGENTS.md | ✓ | ✓ | more than one framework or service |
| ARCHITECTURE.md | — | ✓ | ✓ | more than one module or app |
| CODING-STANDARDS.md | in AGENTS.md | ✓ | ✓ | more than ~10 files expected |
| TESTING.md | in AGENTS.md | ✓ | ✓ | always for M/L |
| SECURITY.md | — | ✓ | ✓ | users, forms, data, or a server |
| DATA-MODEL.md | — | if DB | ✓ | a database exists |
| DESIGN-SYSTEM.md | — | if UI | ✓ | a user interface exists |
| DEPLOYMENT.md | — | ✓ | ✓ | it gets deployed |
| DEPLOY-RUNBOOK.md | — | — | if self-hosted | someone or an agent deploys on a server |
| SEO.md | — | if public | if public | should be found on search engines |
| TRACKING.md | — | — | if marketing | pixels or analytics |
| adr/ | — | ✓ | ✓ | real decisions were made |
| PR template | — | ✓ | ✓ | GitHub is used |

## 3. Required content per doc

Keep each doc as short as it can be while staying specific. Tables beat paragraphs for rules.

### AGENTS.md (English)
1. What we're building (3–5 lines) + links to PRD and ROADMAP.
2. "Read before you code" table: situation → doc.
3. Stack summary (one line) + pointer to STACK.md.
4. Repo layout and dependency direction rules.
5. Commands (install, dev, lint, typecheck, test, e2e, build, check). Mark "available after Phase 0" if not yet scaffolded.
6. How to work: one phase at a time, plan first for multi-file changes, small vertical slices, tests are part of the task, update docs in the same change, ask before (deps, stack, data model, deleting, URLs, production).
7. Definition of done (checklist).
8. Non-negotiable rules: security, code quality, UI (tokens, RTL logical properties if Arabic), language policy.
9. Git: branch naming, Conventional Commits, PR template, CI green.
10. Never do (secrets, disabling tests, unreviewed deps, changing URLs without redirects, destructive DB commands, copying prototypes as code, adding server credentials to GitHub if deploys are pull-only).

### CLAUDE.md (English)
First line `@AGENTS.md` (Claude Code import). Then: session start ritual (read ROADMAP current phase, its "read before" docs, OPEN-QUESTIONS), how to talk to the owner (their language, non-technical framing, report real test numbers), working style (plan mode, narrow checks first, never claim tests passed without running them, stop after two identical failures), visual work checks, record decisions as ADRs.

### docs/PRD.md (owner's language)
Header table (version, date, owner, status) · Overview · Goals with **measurable** targets · Users and what they want · Scope: in / out (with "deferred by owner decision" list) · Functional requirements by area (public side, admin side) · Notifications table · Spam protection · SEO and tracking (summary, link) · Non-functional requirements table (performance budgets, security, accessibility, browsers, availability, backups, privacy law, maintainability, timezone) · Key user stories with acceptance criteria · Initial data to migrate · Link to OPEN-QUESTIONS.

### docs/ROADMAP.md (owner's language)
Status table with legend (⬜ 🟡 🧪 ✅) · general rules (branch per task, PR + CI, tick boxes, the gate runs in CI and results go to the owner) · then per phase: **goal**, **read before starting**, **tasks** (checkboxes), **test gate** (checkboxes, concrete and automatable: unit/integration/e2e/a11y/performance/security checks + any manual owner review).
Phase 0 = foundation (repo, workspace, pinned versions, lint/format/hooks, typecheck, test runner, minimal app skeletons, dev environment, CI, dependency updates, one passing e2e). The last phase = production launch with a launch checklist. Each phase should be completable in days, not months.

### docs/OPEN-QUESTIONS.md (owner's language)
Table: # · question · needed before (phase) · recommendation · status (⬜/✅). When answered, move the decision into the right doc and mark ✅ with the decision text.

### docs/STACK.md
Date verified + sources · table per area (runtime, apps, quality and testing, external services): name · exact version · why / where used · compatibility notes (e.g. "TS 7 not supported by X yet") · upgrade policy (bot PRs, majors need ADR, security patches within 48h).

### docs/ARCHITECTURE.md
System diagram (mermaid) · rendering and caching strategy · repo tree with one-line purpose per folder · module rules (who may import what; where business logic lives) · i18n · request and data flows for forms and critical features (sequence diagram) · domain rules (e.g. server-side pricing) · auth and roles summary · environments table (local/CI/staging/prod: URL, data, how deployed) · observability.

### docs/DATA-MODEL.md
Conventions (localized fields, slugs, visibility, ordering) · reusable field groups · one table per collection or table (field, type, notes) · globals or settings · status transitions if any · **access matrix** (role × resource × CRUD), and a statement that every row is covered by tests.

### docs/DESIGN-SYSTEM.md
Owner decisions (things not to override) · color tokens (brand + semantic) with a contrast table · typography scale · spacing, radius, shadows · layout rules · component specs table · iconography (incl. RTL mirroring rule) · motion (and reduced-motion) · accessibility checklist · link to the visual source of truth in `design/`.

### docs/CODING-STANDARDS.md
Language settings (e.g. TS strict flags) · structure and size limits · naming table · framework-specific rules · errors and logging (mask personal data) · env access through a validated module · dependency policy · formatting and lint · review checklist.

### docs/TESTING.md
Layers table (unit, integration, e2e, a11y, performance, SEO, visual) with tool and location · what must always have tests · commands · test environment (disposable DB, fake email inbox, test keys, deterministic seed, no real personal data, frozen time) · device and locale projects · budgets · CI pipeline order · flaky test policy · manual QA per phase.

### docs/SECURITY.md
Asset → threats → controls table · authN/authZ · input handling · public forms anti-spam (captcha, honeypot, min fill time, rate limits, WAF) · HTTP headers (CSP etc.) · CSRF/CORS · uploads · secrets · personal data and the applicable law (retention, minimization, consent, residency) · supply chain · server and containers · backups · incident response · PR security checklist.

### docs/SEO.md (public sites)
Target searches · URL structure per locale · redirects from the old site (table) · metadata rules · structured data per page type · sitemap and robots · local SEO · performance · content guidelines · measurement · automated checks in CI.

### docs/TRACKING.md (marketing)
Principles (no tracking before consent, no performance hit, one event layer, IDs in settings) · platforms · consent banner behavior · events table mapped per platform · never send PII · server-side events (optional) · tests.

### docs/DEPLOYMENT.md
Server facts (if inspected) · how we fit into existing setups (reverse proxy, ports, isolation, memory limits) · containers · CI/CD model · environment variables table · email deliverability (SPF/DKIM/DMARC, sending limits) · backups (what, how, when, retention, restore drill) · monitoring · launch checklist (incl. DNS migration steps).

### docs/DEPLOY-RUNBOOK.md (self-hosted, deploys by a person or agent)
Hard rules (only touch our folder, no destructive Docker commands, no secrets in output) · server layout · read-only GitHub access · deploy steps and what the script does (backup → pull → migrate → up → smoke tests) · reporting · rollback · reverse-proxy files · suggested permissions for a server agent.

### docs/adr/
`0000-template.md` (status, date, deciders, context, decision, alternatives, consequences) + one ADR per real decision: frontend framework, backend/CMS, database, repo structure, styling approach, hosting, rendering/caching, deploy model…

## 4. Quality bar and final checks

Before showing the docs:
- [ ] No placeholder text left (`<…>`, "TBD", "lorem") except inside clearly marked templates.
- [ ] Names, numbers, features and constraints match the interview exactly.
- [ ] Owner docs in their language; technical docs in English; this policy written in AGENTS.md.
- [ ] Every phase has a gate with concrete checks.
- [ ] Every unknown is in OPEN-QUESTIONS with a phase and a recommendation.
- [ ] All relative links resolve (script it: scan `](path)` targets and check existence).
- [ ] No secrets or personal data anywhere.
- [ ] Versions in STACK.md were verified today, with sources noted.
