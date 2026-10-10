# GitHub onboarding (beginner-friendly)

Go one step at a time. After each step, ask them to tell you what they see. Never ask for or type their password. They sign in themselves in the browser.

## 1. Explain why (3–4 lines, in their language)

> GitHub is like a safe for your project's code:
> - **Every change is saved as a version**, so if anything breaks we can go back.
> - **It's a backup outside your machine**, so if the laptop dies, the project doesn't.
> - **Agents and developers can work on it together** without overwriting each other.
> - **It runs the tests automatically** on every change, so mistakes are caught before they reach your customers.
> And the repository will be **private**: only you, and whoever you invite, can see it.

## 2. Check what exists

Run (or ask them to run) and interpret for them:

```bash
git --version          # is git installed?
gh --version           # is the GitHub CLI installed?
gh auth status         # signed in? which account?
```

## 3. Create an account (only if they have none)

1. Open https://github.com/signup.
2. Use a work email they'll keep long-term. A company project should ideally live under a company email or a GitHub **organization** (free), so ownership stays with the business. Mention this once; respect their choice.
3. Pick a username, verify the email, and choose the **Free** plan.
4. **Strongly recommend turning on two-factor authentication** (Settings → Password and authentication). It's the single best protection for their code.

## 4. Install the tools

**macOS**
```bash
xcode-select --install          # gives git, if missing (they click "Install")
brew install gh                 # if Homebrew exists; otherwise download from https://cli.github.com
```
**Windows**
```powershell
winget install --id Git.Git -e
winget install --id GitHub.cli -e
```
(Or download the installers from https://git-scm.com and https://cli.github.com.)

**Ubuntu/Debian**
```bash
sudo apt update && sudo apt install -y git gh
```

Ask before installing anything system-wide.

## 5. Connect this computer to GitHub

```bash
gh auth login
```
Choose: **GitHub.com** → **HTTPS** → **Login with a web browser**. A one-time code appears. They press Enter, the browser opens, they paste the code and approve. Then:

```bash
gh auth setup-git      # lets plain `git push` use the same sign-in (avoids "repository not found" later)
git config --global user.name  "Their Name"
git config --global user.email "their-email@example.com"   # or the GitHub noreply address
```

Verify: `gh auth status` shows ✓ Logged in.

## 6. Create the repository and push

Confirm the name (lowercase, short, e.g. `my-shop`, `clinic-booking`) and **private** visibility, then:

```bash
git init -b main
git add -A
git status                      # show them what will be uploaded; confirm no .env or secrets
git commit -m "docs: project foundation (PRD, roadmap, agent guides)"
gh repo create <name> --private --source=. --remote=origin --push --description "<one line>"
```

Verify:
```bash
gh repo view <owner>/<name> --json visibility,url
```
Show them the link and tell them to open it: they'll see their files and the commit.

## 7. Explain what they now have

- The repo link, and that it's private.
- From now on every change is a commit with a message; agents work in branches and open pull requests; tests run automatically.
- They can invite collaborators later: Settings → Collaborators.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| `remote: Repository not found` on `git push`, but `gh repo view` works | git isn't using the gh sign-in | `gh auth setup-git`, or once: `git -c credential.helper='!gh auth git-credential' push` |
| `Permission denied (publickey)` | Remote uses SSH, no key added | Switch to HTTPS: `git remote set-url origin https://github.com/<owner>/<name>.git` |
| `gh: command not found` | CLI not installed or not on PATH | Reinstall; restart the terminal |
| `xcrun: error: invalid active developer path` (macOS) | Command Line Tools missing | `xcode-select --install` |
| Push rejected: file too large (>100 MB) | Big binary in the repo | Remove it from the commit; keep large media outside git |
| They accidentally committed a secret | `.env` or a key in history | Rotate the secret immediately, then remove it from history (`git filter-repo`); GitHub secret scanning may also alert them |

## If they don't want GitHub

Respect it. Run `git init` and commit locally anyway (versions still help), explain once that there's no off-machine backup, and record it in `OPEN-QUESTIONS.md`. Offer alternatives: GitLab, Bitbucket, or a private Gitea on their server.
