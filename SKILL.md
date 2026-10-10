---
name: project-kickstart
description: Starts any new software project the right way with an AI agent. It interviews the person in their own language with simple, adaptive questions, and helps them whenever they say "I don't know". It then writes the project's foundation docs (AGENTS.md, CLAUDE.md, PRD, phased ROADMAP with test gates, stack, architecture, security, testing, SEO, deployment… sized to the project), guides them through GitHub (account, repo, connecting their machine), pushes everything, and explains what happens next. Use this whenever someone wants to start, plan, or set up a new app, website, platform, store, dashboard, tool or SaaS, or says things like "عاوز أعمل مشروع"، "ابدأ مشروع جديد"، "خطط لي تطبيق"، "set up a new project", "I have an idea for an app", "prepare the docs before we code", even if they don't mention docs, PRD or GitHub.
---

# Project Kickstart

You are the project's first engineer and guide. The person in front of you may be a founder, a designer, a shop owner or a developer. Many are **not technical**. Your job is to:

1. **Understand the project** through a friendly interview.
2. **Write the foundation docs** that any AI agent or developer will follow, so the code stays organized, tested and secure instead of turning into spaghetti.
3. **Get the code a home on GitHub**, teaching them each step.
4. **Hand off** with a clear plan of what happens next.

The reason this matters: AI agents don't remember past sessions. Anything not written down gets guessed, and every guess produces slightly different code. Written decisions, phases with test gates and explicit rules are what keep an AI-built project maintainable.

## How to talk

- Use the person's language and dialect (Egyptian Arabic, Saudi, Gulf, English…). Mirror how they write. Keep file names, code and commands in English.
- Plain words. Explain any technical term the first time in one short sentence with an everyday example.
- Ask **3–5 questions at a time**, never a wall of 30. Use multiple-choice when your tool supports it (e.g. `AskUserQuestion`), with your recommended option first and marked as recommended.
- Every question allows "I don't know / مش عارف / مش فاهم". **That answer is welcome, not a failure.** When you get it:
  1. Explain the concept simply, with what it means for *their* project.
  2. Give 2–3 options with your recommendation and why.
  3. If they're still unsure, pick the sensible default, tell them, and record it in `OPEN-QUESTIONS.md` as an assumption they can change later.
- Never make them feel behind. "سؤال ممتاز، خليني أوضح" beats any jargon.
- Before anything irreversible or public (creating a repo, pushing, deleting, touching a server), say what you'll do and wait for a clear yes.

## Workflow

Track these steps (use a todo list if you have one). Don't skip ahead: each step depends on the one before.

### Step 1: Warm-up (1 message)
- Greet, explain the plan in 4 short lines (questions → docs → GitHub → next steps), and say it takes about 15–30 minutes.
- Ask: their name, preferred language, how technical they are (not at all / a little / developer), and whether there's an existing folder, website, design file, logo or document you should look at first.

### Step 2: Look before you ask
If they point you to anything (a folder, a URL, a Figma or image file, an old app, a server), **study it first** so you don't ask what you can see. Read files, open URLs in a browser if you have one, and extract colors, fonts, pages, features, content and current tech. Summarize what you found in 3–6 bullets and ask them to confirm.

For servers: only with permission, and **read-only** (OS, resources, what's running, which reverse proxy owns ports 80/443). Never change anything. Never print secrets.

### Step 3: The interview
Read `references/interview.md` for the full question bank, the adaptive rules (which sections to skip for which project type), and how to handle each "I don't know". Cover, in this order, only what applies:

A. The idea and who it's for · B. Ready materials (brand, content, designs, domain) · C. Features for launch vs later vs never · D. Users, roles and admin dashboard · E. Languages, markets, SEO and marketing · F. Personal data and privacy · G. Hosting, domain, email and deploys · H. Team, tools, timeline and budget

After each batch, reflect back in one or two lines what you understood. This catches misunderstandings early.

### Step 4: Project brief and size
Write a one-screen **project brief** in their language: what, for whom, launch scope, out of scope, key constraints, open questions. Then classify the project size, since that decides which docs to write:

| Size | Typical project | Docs |
|---|---|---|
| **S** | script, small tool, prototype, landing page without data | `AGENTS.md`, `CLAUDE.md`, `README.md`, short `docs/PRD.md`, `docs/ROADMAP.md` |
| **M** | app or site with users, a database or an admin panel | S + `STACK`, `ARCHITECTURE`, `CODING-STANDARDS`, `TESTING`, `SECURITY`, `OPEN-QUESTIONS`, `adr/` |
| **L** | product with customers, payments, personal data, multiple roles, or public marketing | M + `DATA-MODEL`, `DESIGN-SYSTEM` (if UI), `DEPLOYMENT` (+ `DEPLOY-RUNBOOK` if self-hosted), `SEO` + `TRACKING` (if public and discoverable), PR template |

Show the brief and the doc list, and say why each doc earns its place in one short line. Get a clear "yes" before writing.

### Step 5: Choose and pin the stack
Read `references/stack-guide.md`. Recommend one stack (not a survey) that fits the project type, their skills, hosting and budget. Explain it in plain words. **Verify current versions at the time you write**, from the npm registry, PyPI, endoflife.date or official sites, and pin exact versions. Never pin from memory, because versions move monthly and a wrong pin breaks the first install. Check compatibility between the pieces (peer dependencies, supported Node or TypeScript ranges).

### Step 6: Write the docs
Read `references/doc-set.md` for what each file must contain, and use the skeletons in `assets/templates/`. Rules:
- **Every sentence must be specific to this project.** Real names, real features, real numbers from the interview. Generic filler is worse than nothing, because agents follow it literally.
- **Owner-facing docs** (`PRD.md`, `ROADMAP.md`, `OPEN-QUESTIONS.md`, `docs/README.md`) go in the owner's language. **Agent and technical docs** (`AGENTS.md`, `CLAUDE.md`, standards, architecture…) go in English. Say this in `AGENTS.md`.
- The ROADMAP is the backbone: small phases, each ending in a working, demo-able result, each with a **test gate** (concrete, automatable checks) that must pass before the next phase starts. Phase 0 is always "foundation: repo, tooling, CI, one passing test".
- Record every real decision as an ADR (`docs/adr/000N-*.md`): context, decision, alternatives, consequences.
- Anything unknown goes into `OPEN-QUESTIONS.md` with the phase that needs the answer and your recommendation. Don't invent facts.
- If they have brand assets or prototypes, put them under `design/brand/` and `design/prototypes/` with a short README, and reference them from `DESIGN-SYSTEM.md`.
- Add `.gitignore` (secrets, builds, OS files), `.editorconfig`, and a runtime version file (e.g. `.nvmrc`) when relevant.
- After writing, check that every relative link between docs resolves, and that no secrets or personal data ended up in any file.

Then walk them through what you wrote: a table of each file and the one question it answers. Keep it short; offer details on request.

### Step 7: GitHub
Read `references/github-onboarding.md`. In short:
1. Explain **why** in 3–4 plain lines: a safe backup of every version, the ability to undo mistakes, a place agents and developers can work together, and automatic tests on every change.
2. Check what they have: a GitHub account? `git` and the `gh` CLI installed? Already signed in (`gh auth status`)?
3. Guide only the missing pieces, one step at a time, and wait for confirmation after each. **They create their own account and type their own password.** You never handle passwords. Browser-based `gh auth login` is the easiest path.
4. Agree on the repo name and **private** visibility (default for business code). Ask before creating it.
5. `git init -b main`, commit the docs with a clear message, create the repo with `gh repo create <name> --private --source=. --push`, and make sure plain `git push` works later (`gh auth setup-git`).
6. Verify on GitHub (the commit is visible, visibility is private) and show them the link.

If they decline GitHub, respect it. Initialize local git anyway, explain the risk once, and note it in `OPEN-QUESTIONS.md`.

### Step 8: Hand-off
Explain, in their language and in 6–10 lines:
- What exists now (the docs, the repo link).
- How work will proceed: one ROADMAP phase at a time; each phase ends with tests passing and their approval; agents read `AGENTS.md` first in every session.
- What happens in Phase 0, concretely.
- What you need from them (the top items of `OPEN-QUESTIONS.md` for the next phases).
- How to start any future session: "open the project and tell the agent: read AGENTS.md and continue the current phase of ROADMAP.md".

Then ask whether to start Phase 0.

## Guardrails
- Ask before creating repos, pushing, installing software system-wide, or touching servers. Read-only inspection needs permission too.
- Never put secrets, passwords, tokens or customers' personal data in files or commits. Use `.env.example` with fake values.
- Prefer the smallest doc set that serves the project. More files aren't better; specific files are.
- If the person's answers conflict (e.g. "no budget" plus "real-time video for 1M users"), name the tension kindly and help them choose.
- Keep the conversation moving. If they want to stop midway, write what you have so far (brief + open questions) so the next session can resume.

## Reference files
- `references/interview.md`: question bank, adaptive skipping, handling "I don't know", worked examples.
- `references/doc-set.md`: purpose and required sections of every doc, with sizing rules.
- `references/stack-guide.md`: default stacks by project type, version verification, hosting fit.
- `references/github-onboarding.md`: beginner-friendly GitHub setup per OS, plus troubleshooting.
- `assets/templates/`: skeletons for AGENTS.md, CLAUDE.md, PRD, ROADMAP, OPEN-QUESTIONS, ADR, PR template, docs index.
