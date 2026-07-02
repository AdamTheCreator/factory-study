# AGENTS.md — Ready-to-Use Template

> Copy this into the root of your demo/sandbox repo, delete what doesn't apply, and fill
> in the specifics. Rule of thumb: **only document what a new senior hire couldn't figure
> out from reading one file** — the agent can discover the obvious stuff itself.
> Keep it under ~150 lines; this file is loaded into context on every session.

---

# AGENTS.md

## Project Overview
<!-- One paragraph. What this is, who uses it, the one architectural fact that matters. -->
This is a <type of app> serving <who>. The critical thing to understand:
<e.g., "all state flows through the event bus in src/events — nothing mutates directly">.

## Build & Commands
- Install: `pnpm install`
- Dev server: `pnpm dev` (http://localhost:3000)
- Test all: `pnpm test`
- Test one file: `pnpm test -- path/to/file.test.ts`
- Typecheck: `pnpm typecheck` — run before claiming any task is done
- Lint + format: `pnpm lint && pnpm format` — MUST pass before commit

## Project Layout
- `apps/web/` — frontend (<framework>)
- `packages/api/` — API layer; routes/routers live in `packages/api/src/routers/`
- `packages/db/` — schema + migrations. Migrations are generated (`pnpm db:generate`), never hand-edited.
- `packages/shared/` — types/utils shared across packages. Changes here affect everything.

## Development Patterns
- <Pattern 1 — e.g., "All DB access goes through repository functions in packages/db/repos — no raw queries in route handlers.">
- <Pattern 2 — e.g., "Throw AppError with an error code, never bare Error.">
- <Pattern 3 — e.g., "Feature flags via flags.ts; never branch on env vars directly.">
- When adding a feature, find the closest existing example and follow its structure.

## Testing Expectations
- New logic needs unit tests next to the file (`*.test.ts`).
- Bug fixes need a regression test that fails without the fix.
- Don't weaken or delete a failing test to make it pass — fix the code or flag the conflict.

## Git Workflow
- Branches: `feat/<slug>`, `fix/<slug>`. Conventional commit messages.
- Never commit directly to `main`. PRs require green CI.
- Keep commits scoped: one logical change per commit.

## Security & Data
- Never log secrets, tokens, or PII.
- All mutations require the auth middleware (`withAuth()` / equivalent).
- Secrets come from env/secret manager only — never hardcode, even in tests.

## Things That Will Bite You
<!-- The gold section. Non-obvious landmines. -->
- <e.g., "The dev DB seeds are stale — run pnpm db:seed after schema changes.">
- <e.g., "apps/web has its own tsconfig; editor errors there don't match CI.">
- <e.g., "Do not touch src/legacy/ — scheduled for deletion, changes won't be reviewed.">

---

## Why each section exists (delete this part in your copy)

| Section | What it prevents |
|---------|-----------------|
| Build & Commands | Agent guessing `npm` vs `pnpm`, not knowing how to run one test |
| Project Layout | Agent putting code in the wrong package |
| Development Patterns | Plausible-but-wrong code that ignores house conventions |
| Testing Expectations | "Done" without tests, or tests weakened to pass |
| Git Workflow | Commits to main, mega-commits |
| Security & Data | The demo-killing mistake (logging a secret) |
| Things That Will Bite You | The failures that make people say "the AI doesn't get our codebase" |

**Demo tip:** the fastest credible AGENTS.md is `droid` → *"Read this codebase and draft an
AGENTS.md following the AGENTS.md standard"* → then you spend 10 minutes cutting it down to
high-signal. Show the before/after task quality — that's the whole grounding story in one artifact.
