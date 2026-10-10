<!-- TEMPLATE. Write in the OWNER'S language. Phases should take days, not months. -->
# <Roadmap and test gates>

No phase starts until the current phase's **test gate** passes and the owner approves. Each phase ends with something that works and can be demoed.

## Status
| # | Phase | Status |
|---|---|---|
| 0 | Foundation: repo, tooling, CI | ⬜ |
| 1 | <…> | ⬜ |
| N | Production launch | ⬜ |

Legend: ⬜ not started · 🟡 in progress · 🧪 testing · ✅ approved by owner

### Rules for every phase
- Each task in a branch `phase-<n>/<topic>`, merged via PR after CI passes.
- Tick tasks here when done.
- The gate runs in CI; results (real numbers) go to the owner with a demo link or video.
- Any bug found later gets a regression test.

---

## Phase 0: Foundation
**Goal:** organized repo and quality tools before any feature.
**Read before starting:** AGENTS.md, ARCHITECTURE.md, STACK.md, CODING-STANDARDS.md, TESTING.md

**Tasks**
- [ ] git + GitHub, protect `main` (no direct push, CI required)
- [ ] Workspace structure, exact versions from STACK.md, runtime version file
- [ ] Strict types, lint, format, git hooks, commit message lint
- [ ] Test runner + one unit test; validated env module
- [ ] Minimal app skeleton(s) running locally
- [ ] Local services via Docker (DB, fake email inbox…)
- [ ] CI: install → lint → typecheck → unit → build → e2e smoke
- [ ] Dependency update bot + security scanning
- [ ] `.env.example` documented

**Test gate**
- [ ] Clean clone: install + check + build pass locally and in CI
- [ ] One command starts the dev environment
- [ ] One e2e test passes <in each language/direction if applicable>
- [ ] A PR with a lint error is blocked from merging

---

## Phase 1: <name>
**Goal:** <one line>
**Read before starting:** <docs>

**Tasks**
- [ ] <task>

**Test gate**
- [ ] <unit tests for …>
- [ ] <integration: …>
- [ ] <e2e journey: …>
- [ ] <a11y / performance budget / security check>
- [ ] <owner review of …>

---

## Phase N: Production launch
**Tasks:** server/hosting, domain and DNS, TLS, backups, monitoring, email DNS (SPF/DKIM/DMARC), data migration, search console, staff training.
**Gate (launch checklist):** restore drill passed · security scan clean · smoke tests on production · redirects verified · emails reach inbox · owner approval.
