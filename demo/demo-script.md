# The 20-Minute Demo Script (7-Step Arc)

> A verbatim-ish script for the demo arc in note 05. Rehearse it until you can deliver it
> conversationally and survive interruptions. Times assume a prepared sandbox repo with an
> AGENTS.md already written and a seeded bug + feature idea.
>
> **Prep checklist (before anyone joins):** terminal font huge · sandbox repo clean ·
> `droid` logged in · AGENTS.md committed · a known small bug reproducible · notifications off.

---

## Cold open (1 min)

> "Before I show anything: Factory's bet is that the model is table stakes — the hard part
> is safely *delegating* real engineering work across a real org. So everything you'll see
> is about three things: **grounding** the agent in your codebase, **controlling** how much
> it can do, and making it **infrastructure**, not a toy. Twenty minutes, and you drive one
> of the steps yourself."

## Step 1 — Ground it (3 min)

Do: `cd sandbox-repo && droid`, then `/context`.

> "First failure mode of every coding agent: it doesn't know your conventions. Most agent
> failures are context failures. This is `/context` — exactly what the Droid is holding,
> token by token. The anchor is this file —" *(open AGENTS.md)* "— an open standard, not
> Factory-proprietary. Build commands, layout, house patterns, the landmines. Droid can
> draft it for you in a minute; your seniors edit it once and every agent session inherits it."

If asked "what if we have a huge monorepo?" → context compression: it keeps high-confidence
anchors and pulls detail on demand, rather than stuffing the window.

## Step 2 — Small win, controlled (3 min)

Do: stay at low autonomy. Prompt the seeded bug: *"Fix the <bug> in <file> — minimal change,
add a regression test."* Show the approval prompts, then the diff.

> "Notice it's asking permission for every action — I'm at **low autonomy**. This dial —"
> *(Ctrl+L)* "— is org policy, not vibes: read-only by default, `low` for safe edits,
> `medium` for typical dev work, `high` for push/deploy. It's how 'let an agent loose on
> our repo' gets through your security review: you start read-only and earn each level."

## Step 3 — Plan a real feature: Spec Mode (4 min)

Do: `droid --use-spec "<real feature>"` (or Shift+Tab into plan mode). Let the spec render.
Open the saved file in `.factory/docs/`.

> "For non-trivial work you don't want the agent improvising. Spec Mode produces a
> reviewable plan first — acceptance criteria, technical approach, the exact files it'll
> touch. You review the *design*, not every keystroke. It's saved as markdown in the repo,
> so the plan is an artifact, not a chat scroll. Approve it, and it executes against it."

**→ Hand them the keyboard here.** Have the prospect edit one line of the spec or reject a
step. Hands on keyboard converts.

## Step 4 — Go big: Missions (2 min — narrate, don't wait)

Do: kick off `/missions` on the larger task (or show a completed one).

> "When it's a migration or a multi-day feature, Mission Mode splits the work across
> agents — a **worker** does the work, a **validator** checks it. An agent reviewing an
> agent is a built-in quality gate. This is delegation at project scale, and it runs in
> the web app too, so it doesn't need your laptop open."

## Step 5 — Make it infrastructure: droid exec (3 min)

Do: show the GitHub Action YAML, then a green run.

```yaml
- run: droid exec --auto medium -o json "fix lint and organize imports on changed files"
```

> "Same agent, headless. This is where it stops being individual productivity and becomes
> team leverage: CI steps, cron jobs, pre-commit hooks. JSON out, so your pipeline consumes
> the result. Every convention from that AGENTS.md still applies here — one context layer,
> every surface."

## Step 6 — Close the loop: /review (2 min)

Do: `/review` on the branch from steps 2–3.

> "And before any of this reaches a human reviewer: `/review` runs your rubric — security,
> performance, standards — as reusable guidance, consistently, on every change. Humans keep
> the judgment calls; the agent catches the mechanical 80%. For UI work, Droid Control can
> actually drive a browser and verify the flow end to end."

## Step 7 — Zoom out (2 min)

Do: switch to slides/web app — Agent Readiness dashboard, enterprise page.

> "Last thing. Adoption isn't a download, it's a maturity curve — **Agent Readiness** scores
> each repo (conventions documented? tests trustworthy? CI clean?) and gives you the roadmap.
> And the governance layer your security team will ask about is native: SSO/SCIM, audit,
> hierarchical org→project→user policy, EU deployment — and **BYOK**, so this runs on *your*
> model contracts, Anthropic or OpenAI or open models you host yourself. No lab lock-in."

## Close (30 sec)

> "So: grounded in your conventions, autonomy you dial up as trust builds, and one governed
> agent from laptop to CI. The natural next step is a two-week POC on one repo you pick —
> we define the success metric up front. What repo would you want to try it on?"

*(That last question is the close. Always end on it.)*

---

## Interruption playbook

| They say | You say |
|----------|---------|
| "We use Cursor already" | "Keep it — Cursor's a great editor. This is the delegation + governance layer across CLI/CI/web. Different altitude; they coexist." (note 06 one-liners) |
| "What if it hallucinates?" | Point at the screen: read-only default, spec review, validator agents, `/review`. "You saw every gate in the last 15 minutes." |
| "How much does it cost?" | Directional: usage-based, free tier up through enterprise — "let me confirm current numbers rather than misquote" (then actually follow up). |
| "Can it use our fine-tuned model?" | BYOK incl. self-hosted (Ollama, Baseten, Fireworks…). Mixed models: strong model plans, cheap model executes. |
| Demo breaks | Narrate honestly, fall back to the pre-recorded run. Never fake it — technical buyers smell it. |
