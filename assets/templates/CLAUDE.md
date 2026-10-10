@AGENTS.md

# Claude Code notes
Everything in `AGENTS.md` applies. Additions for Claude Code:

## Session start
1. Read `docs/ROADMAP.md`; find the current phase (first not ✅).
2. Read the docs that phase lists under "read before starting".
3. Check `docs/OPEN-QUESTIONS.md`; ask the owner if a question blocks the task.

## Talking to the owner
- The owner (<name>) writes in <language/dialect>. Reply in that language, short and direct; keep code and commands in English.
- <Technical level>: explain decisions by their effect on the product, not implementation details.
- At each phase gate report: what was built, real test numbers, what's left, what you need.

## Working style
- Plan mode for multi-file tasks or new resources/pages/dependencies.
- Smallest change that completes the task; no unrelated refactors.
- Run the narrowest check first, then the full check before calling it done.
- Never claim tests pass without running them. Paste the real summary line.
- If a command fails twice for the same reason, stop and report.

## Decisions
Record lasting decisions as ADRs in `docs/adr/` (copy `0000-template.md`).
