# 04 — Workflows: Spec, Missions, Exec, Review

These are the capabilities you'll actually *demo*. For each: know what it is, when to reach
for it, and the one-line "why a customer cares."

## 1. Specification Mode (`--use-spec` / Plan mode)

**What:** Before touching code, Droid produces a complete **spec** — implementation plan,
acceptance criteria, technical details, the list of files it'll change. You review/refine,
then it executes. Approved specs are saved as markdown in **`.factory/docs/`**.

**When:** Any non-trivial feature; anything where "measure twice, cut once" matters; anytime
a customer is nervous about letting an agent loose.

**Why customers care:** It turns an opaque agent into a reviewable plan. The human stays in
control at the *design* level, not babysitting every keystroke. Great trust-builder in a demo.

```bash
droid --use-spec "add rate limiting to the public API"
droid --use-spec --spec-model <stronger-model> "migrate auth from sessions to JWT"
```

Tip: use `--spec-model` to plan with a stronger/more expensive model, then execute with a
cheaper/faster one. Good cost story.

## 2. Mission Mode (`--mission` / `/missions`)

**What:** Multi-agent orchestration for large work. Work is split across agents — typically
a **worker** that does the work and a **validator** that checks it — coordinated as a
structured, multi-step mission. Available in the CLI and the Web app.

**When:** Big features, multi-file migrations, anything too large for one linear pass.

**Why customers care:** This is the "Droid army" story — delegate a project, not a snippet.
The worker/validator split is a built-in quality gate (an agent reviewing an agent).

Docs break Missions into **planning → validation → configuration → troubleshooting** — know
that there's structure here, not just "turn it on."

## 3. Droid Exec (headless / `droid exec`)

**What:** Non-interactive Droid for automation. Covered mechanically in note 02; here's the
*workflow* lens.

**Patterns:**
- **CI gate:** `droid exec --auto medium "run tests; if any fail, fix and re-run"` in a GitHub Action.
- **Scheduled hygiene:** cron `droid exec "organize imports and fix lint across changed files"`.
- **Pre-commit hook:** `droid exec --auto low "format and lint staged files"`.
- **Pipeline step:** `droid exec -o json "audit deps for CVEs"` → parse JSON downstream.

**Why customers care:** The agent isn't just an IDE toy — it becomes infrastructure. This is
the wedge from "individual productivity" to "platform/team automation" (and bigger deals).

Docs include build guides for **Droid Exec apps, GitHub Actions, lint fixes, import
organization, VPS deployment** — point customers there for recipes.

## 4. Code Review (`/review`)

**What:** Reviews uncommitted changes, a PR, or specific commits for security, performance,
and standards — using **reusable guidance** patterns (your review rubric, encoded).

**When:** Pre-PR self-review; automated PR review in CI; enforcing standards at scale.

**Why customers care:** Consistent, tireless first-pass review that catches the obvious stuff
so humans focus on judgment calls. Pairs with **Automations** in the web app for PR management.

```text
/review                       # review my uncommitted changes
# or wire automated review on PRs via the web app's Automations
```

## 5. Droid Control (desktop/browser automation)

**What:** Drives terminals, browsers, and desktop apps for **QA and validation** — e.g.,
"click through the signup flow and confirm it works," not just unit tests.

**When:** End-to-end validation, UI QA, reproducing a user-reported bug in a real browser.

**Why customers care:** Closes the loop — the agent can *verify its own work* against a
running app, not just assert that code compiles.

## 6. Supporting capabilities to name-drop

- **Agent Readiness** — score + dashboard for how prepared a repo/org is for agents (→ note 05; big SE wedge).
- **AutoWiki** — auto-generated, maintained wiki/docs of a codebase.
- **Automations** — web-app CI workflows, repo scanning, PR management.
- **Skills** — reusable capabilities (data analysis, QA automation, browser automation,
  frontend UI, internal tools, PM). Invoke via `/skills`.
- **Custom Droids** — define specialized agents for recurring workflows (→ note 05/level 400).

## Choosing the right tool (decision cheat-sheet)

| Situation | Reach for |
|-----------|-----------|
| Small, well-understood fix | Default/auto mode, low autonomy |
| Non-trivial feature, want a plan first | **Spec Mode** |
| Large feature / migration | **Missions** |
| Repeatable automation, CI, cron | **Droid Exec** |
| Quality gate on changes/PRs | **`/review`** + Automations |
| Verify behavior in a real UI | **Droid Control** |
| "Are we even ready for agents?" | **Agent Readiness** report |

## Hands-on rep

1. Run a real feature through **Spec Mode** end to end; show the saved spec in `.factory/docs/`.
2. Kick off a **Mission** on something bigger; watch the worker/validator split.
3. Wire **`droid exec`** into a GitHub Action on a throwaway repo.
4. Run **`/review`** on a messy branch and read the findings.

## Self-check (Level 300)

- [ ] I can demo Spec Mode and explain the trust/control story.
- [ ] I can explain worker/validator Missions and when they beat a single pass.
- [ ] I built a working `droid exec` CI step.
- [ ] I can match each customer scenario to the right workflow without hesitating.

Sources: [Specification mode](https://docs.factory.ai/cli/user-guides/specification-mode) ·
[Missions](https://docs.factory.ai/cli/features/missions) ·
[Droid Exec](https://docs.factory.ai/cli/droid-exec) ·
[Code review](https://docs.factory.ai/cli/features/code-review)
