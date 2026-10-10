# Project Kickstart

**Start any software project the right way with an AI agent.**

An [Agent Skill](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) (and a standalone prompt for any AI agent) that interviews you about your project in your own language, writes the foundation docs your AI agents will follow, puts everything on GitHub, and explains what happens next.

[العربية](README.ar.md) · Made by **[Motalim](https://github.com/motalim-ai)**

---

## Why

AI coding agents don't remember past sessions. Anything that isn't written down gets guessed, and every guess produces slightly different code. After a few weeks, that's spaghetti.

Project Kickstart fixes this before the first line of code. It writes down **what** you're building, **in what order**, **with which tools**, and **which rules** every agent must follow, including tests that must pass before moving to the next phase.

## What it does

1. **Interviews you**, 3–5 simple questions at a time, in your language and dialect. It skips what doesn't apply (no SEO questions for an internal tool).
2. **Helps when you don't know.** Say "I don't know" and it explains the concept with an example from *your* project, recommends an option, and records the assumption so you can change it later.
3. **Looks before it asks:** your existing website, logo, designs or server (read-only, with permission).
4. **Writes a project brief** and waits for your approval.
5. **Picks a stack** and verifies the *current* versions at that moment, not from memory.
6. **Writes right-sized docs:**

   | Size | Example | Docs |
   |---|---|---|
   | **S** | script, prototype, simple landing page | `AGENTS.md`, `CLAUDE.md`, `README.md`, short PRD, ROADMAP |
   | **M** | app or site with users, database or admin panel | + STACK, ARCHITECTURE, CODING-STANDARDS, TESTING, SECURITY, OPEN-QUESTIONS, ADRs |
   | **L** | customers, payments, personal data, roles, public marketing | + DATA-MODEL, DESIGN-SYSTEM, DEPLOYMENT, DEPLOY-RUNBOOK, SEO, TRACKING, PR template |

   The **ROADMAP** splits the work into small phases, each with a **test gate** that must pass before the next phase starts.
7. **Sets up GitHub** step by step: why it matters, creating an account (you type your own password), connecting your machine, creating a **private** repo, and pushing.
8. **Hands off** with a clear plan: how work proceeds phase by phase, what you need to provide, and how to resume in any future session.

## Install

### Claude Code
```bash
git clone https://github.com/motalim-ai/project-kickstart ~/.claude/skills/project-kickstart
```
Then, in any new folder, say *"I want to start a new project"*, or run `/project-kickstart`.

To update later: `git -C ~/.claude/skills/project-kickstart pull`

### Claude app / Claude.ai
Download `project-kickstart.skill` from the [latest release](https://github.com/motalim-ai/project-kickstart/releases/latest) and add it in **Settings → Capabilities → Skills**.

### Any other agent (ChatGPT, Cursor, Codex, Gemini, Copilot…)
Copy the contents of [`PROMPT.md`](PROMPT.md) and paste them as your first message. It's self-contained. Agents that can read and write files and run terminal commands get the most out of it.

## What's inside

| File | Purpose |
|---|---|
| [`SKILL.md`](SKILL.md) | The workflow the agent follows |
| [`references/interview.md`](references/interview.md) | Question bank, skip rules, how to handle "I don't know" |
| [`references/doc-set.md`](references/doc-set.md) | Every doc: when to include it and what it must contain |
| [`references/stack-guide.md`](references/stack-guide.md) | Default stacks per project type, hosting fit, version verification |
| [`references/github-onboarding.md`](references/github-onboarding.md) | Beginner-friendly GitHub setup for macOS, Windows and Linux, plus troubleshooting |
| [`assets/templates/`](assets/templates) | Templates for AGENTS.md, CLAUDE.md, PRD, ROADMAP, OPEN-QUESTIONS, ADR, PR template |
| [`PROMPT.md`](PROMPT.md) | Single-prompt version for any agent |

## Principles

- **Specific beats long.** Every line must be about *your* project. Generic filler is worse than nothing, because agents follow it literally.
- **Small phases, real tests.** No phase starts until the previous one's tests pass and you approve.
- **Decisions are written down** as ADRs, so nobody reopens settled questions.
- **Owner docs in your language, technical docs in English.**
- **Safe by default:** private repos, no secrets in files, permission before anything irreversible, read-only server inspection.

## Contributing

Issues and pull requests are welcome, especially new interview examples, stack defaults for more project types, and translations.

## License

[MIT](LICENSE) © Motalim
