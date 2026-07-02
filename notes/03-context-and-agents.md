# 03 — Context, AGENTS.md & Memory

> This is the highest-leverage note in the guide. The single biggest predictor of "Droid
> did great" vs. "Droid went sideways" is **context quality**. As an SE, teaching customers
> to ground the agent is most of the value you deliver. Master this.

## The context stack (how Droid stays grounded)

Droid assembles context from layers, roughly:

1. **AGENTS.md** — your repo's conventions, encoded for agents (the foundation).
2. **Dynamic code search** — intelligent file discovery; it reads the relevant parts of
   the codebase on demand rather than ingesting everything.
3. **Tool / MCP integrations** — GitHub, Jira/Linear, Sentry, Slack, Notion → pulls in
   tickets, incidents, design decisions, acceptance criteria.
4. **Organizational memory** — persistent team conventions that carry across sessions.

The SE story: *"You're not prompting harder, you're grounding better."* Most failures are
context failures, not model failures.

## AGENTS.md — the foundation file

`AGENTS.md` is an emerging **open standard** (not Factory-proprietary — also used by other
agents) placed at the repo root. It tells the agent how to work with *your* project:
the non-obvious conventions a new senior hire would need.

**What to put in it:**

```markdown
# AGENTS.md

## Build & Commands
- Install: `pnpm install`
- Dev: `pnpm dev`
- Test: `pnpm test` (Vitest). Run a single test: `pnpm test -- <file>`
- Lint/format: `pnpm lint && pnpm format` — MUST pass before commit.

## Project Layout
- `apps/web` — Next.js frontend
- `packages/api` — tRPC API; routers live in `packages/api/src/routers`
- `packages/db` — Drizzle schema; migrations are generated, never hand-edited.

## Development Patterns
- Prefer server components; mark client components explicitly.
- All DB access goes through repository functions in `packages/db/repos` — no raw queries in routes.
- Errors: throw `AppError`, never bare `Error`.

## Git Workflow
- Branch naming: `feat/…`, `fix/…`. Conventional commits.
- Never push to `main`. Open a PR; CI must be green.

## Security
- Never log secrets or PII. Auth via `withAuth()` middleware on every mutation.

## Performance
- Avoid N+1 queries; batch with the dataloader in `packages/db/loaders`.
```

**Rules of thumb:**
- Keep it **concise and high-signal** — it's loaded into context, so bloat costs tokens and dilutes focus.
- Document the **non-obvious** (the stuff that isn't discoverable from reading one file).
- Treat it like code: review it, keep it current, put it in version control.
- You can have **nested/hierarchical** AGENTS.md (org → project → subdir) with extension-only
  semantics — deeper files add to, not silently override, broader ones.
- A great Droid trick: *"Read the codebase and draft an AGENTS.md for it,"* then you edit.

## Context compression & "context confidence"

Factory uses **context compression** so Droid can work across large codebases without
blowing the window: it keeps anchor points / high-confidence context and compresses the
rest, restoring detail when needed. Practical implication for customers: it scales to big
monorepos better than naive "stuff everything in the prompt" tools.

Use **`/context`** in the REPL to *show* a customer exactly what's loaded and how tokens are
spent — a fantastic teaching moment in a demo.

## Memory management

- **Organizational memory** persists conventions and decisions across sessions and teammates,
  so the team converges on consistent practices instead of re-explaining context every time.
- Combined with AGENTS.md + integrations, this is how Factory turns "a smart intern each day"
  into "a teammate who remembers."

## MCP & integrations (feeding context in)

```bash
droid mcp add <name> <url>     # register an MCP server
# in-REPL: /mcp to manage servers
```

Connecting **GitHub, Jira/Linear, Sentry, Slack, Notion** lets Droid pull acceptance
criteria, incident history, and architectural decisions automatically — so when you say
*"implement LINEAR-1234,"* it actually knows what that means.

## Rules, conventions & token efficiency (power-user layer)

Factory's docs cover **rules & conventions**, **prompt crafting**, **token efficiency**, and
**context compression** as distinct power-user topics. The throughline:
- Put durable rules in AGENTS.md / rules files, not in every prompt.
- Be specific in prompts (paths, acceptance criteria, "don't touch X").
- Watch `/context` and `/cost`; trim what you don't need.

## Hands-on rep

1. On a real repo, run `droid` → *"Draft an AGENTS.md for this project."* Edit it down to high-signal.
2. Re-run a task with vs. without the AGENTS.md and note the quality/▢diff difference. (This
   before/after is **gold** for a demo — show it.)
3. Wire one MCP integration (GitHub is easiest) and ask Droid about a real PR/issue.
4. Open `/context` and narrate where the tokens go.

## Self-check (core of Level 300)

- [ ] I can write a clean, high-signal AGENTS.md from scratch.
- [ ] I can explain context compression and why it helps on large codebases.
- [ ] I can demo `/context` and explain the token breakdown.
- [ ] I can articulate "most failures are context failures" with a concrete example.

Sources: [AGENTS.md config](https://docs.factory.ai/cli/configuration/agents-md) ·
[Context compression](https://docs.factory.ai/cli/power-user/context-compression) ·
[Memory management](https://docs.factory.ai/cli/power-user/memory-management) ·
[MCP](https://docs.factory.ai/cli/configuration/mcp)
