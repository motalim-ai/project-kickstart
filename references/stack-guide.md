# Choosing and pinning the stack

## Principles
- **Recommend one stack**, explained in plain words. A comparison table is fine *after* the recommendation if they ask.
- **Fit beats fashion:** match the project type, who maintains it, the hosting they already have, and the budget.
- **Boring and well-documented wins.** AI agents write better code in popular, stable tools with lots of public examples.
- **Few moving parts.** Every extra service is something to secure, update and pay for.
- **Record the choice as an ADR** with the alternatives considered.

## Defaults by project type (starting points; adjust to the person)

| Project | Recommended starting stack | Why |
|---|---|---|
| Content or marketing site (SEO matters), few interactive bits | **Astro** + plain CSS design tokens; content in Markdown, or a headless CMS if staff edit it | Fastest pages, minimal JS, great SEO |
| Site + admin dashboard for non-technical staff (menu, branches, orders) | **Astro** (public) + **Payload CMS** (admin + API) + **PostgreSQL**, pnpm monorepo | Generated admin UI in many languages incl. Arabic RTL, code-first schema, self-hostable, MIT |
| SaaS / web app with accounts and lots of interactivity | **Next.js** + PostgreSQL (Drizzle or Prisma) + an auth library | One framework for UI and API, huge ecosystem |
| Internal tool / dashboard | Next.js or Payload (if mostly CRUD) + PostgreSQL | CRUD screens come almost free with Payload |
| Mobile app | **Expo (React Native)** + a backend from the rows above | One codebase for iOS and Android |
| API only | Node (Fastify or Hono) or Python (FastAPI) + PostgreSQL | Typed, fast, simple to test |
| Script / automation | Python or Node, single repo, no framework | Smallest thing that works |
| E-commerce, no developer | Shopify / Salla / Zid (hosted) instead of custom code | Payments, inventory and support solved; say so honestly |

Always include: TypeScript strict (for JS stacks), a test runner (Vitest or pytest), Playwright for user journeys, ESLint + Prettier (or Ruff for Python), Docker for local services and deployment, GitHub Actions for CI, and Renovate or Dependabot for updates.

## Hosting fit

| They have | Recommend |
|---|---|
| A VPS (Hostinger, DigitalOcean, Hetzner…) | Docker Compose. Inspect read-only first: if a reverse proxy (Nginx, Traefik, Caddy, a panel) already owns 80/443, plug into it instead of adding another. Set memory limits if the server is shared. Put Cloudflare in front. |
| Nothing, small budget, simple site | A managed static or Node host (Vercel, Netlify, Cloudflare Pages) |
| Nothing, app + database | Railway, Render or Fly.io, or a small VPS if they want fixed costs and data control |
| Data-residency requirement | A provider with a data center in that country; note it in SECURITY.md |

**Deploy model:** ask who should be able to deploy. Pull-based deploys (the server or an on-server agent pulls tested images on request) keep server credentials out of GitHub, which is good for shared servers. Push-based CI deploys are more convenient. If chosen, restrict the key to a forced command.

## Verifying versions (do this every time)

Versions change monthly. Check at the moment of writing and note the date and sources in STACK.md.

```bash
# npm packages: latest version, publish date, engines, peer deps
npm view astro version time.modified engines --json
npm view @payloadcms/next peerDependencies --json

# or, without npm installed, the registry over HTTP:
curl -s https://registry.npmjs.org/astro/latest | jq '{version, engines, peerDependencies}'

# Node LTS
curl -s https://nodejs.org/dist/index.json | jq '[.[] | select(.lts)][0] | {version, lts, date}'

# Databases and runtimes support windows
curl -s https://endoflife.date/api/postgresql.json | jq '.[0:3]'

# Python packages
curl -s https://pypi.org/pypi/fastapi/json | jq '.info.version'
```

Then:
- Check **peer ranges** (e.g. a CMS that supports only Next `>=16.3 <17`) and **tooling support** (e.g. a type checker that supports TypeScript 5–6 but not 7). Pin to the newest version that every piece supports.
- Avoid betas and majors released in the last ~2 weeks.
- Pin exact versions (no `^`/`~`), commit the lockfile, and set the runtime version in `.nvmrc`/`packageManager`/Docker images.
