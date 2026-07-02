# 01 — What Factory Is

## The one-sentence pitch

> **Factory is an AI-native software development platform.** You delegate complete
> engineering tasks — refactors, migrations, incident response, code review, feature
> work — to an agent called a **Droid** that works *everywhere you already work*
> (terminal, IDE, CI/CD, web) without forcing you to change tools, models, or workflow.

Internalize the framing: it's not an autocomplete and it's not "a smarter chatbot."
The mental model Factory sells is **task delegation**. You hand off a unit of work; the
Droid plans it, executes it across many files, runs tests, and reports back — with you
controlling how much it can do autonomously.

## Why it exists (the thesis)

The bet: as models get good enough to complete real tasks, the bottleneck moves from
*"can the model write the code?"* to *"can you safely delegate to it at scale across a
real org?"* That requires:

1. **The same agent everywhere** — laptop, CI, web — not three disconnected tools.
2. **Grounding in your codebase** — conventions, architecture, institutional knowledge.
3. **Governance** — autonomy controls, audit, identity, model routing, data policy.
4. **Model independence** — don't get locked to one lab; route to the best model per task.

Factory's whole product surface is organized around those four needs. As an SE, that's
your story arc: *"the model is table stakes; the platform around it is the product."*

## The four surfaces (know these cold)

| Surface | What it is | Primary user / use |
|---------|-----------|--------------------|
| **Droid CLI** | Terminal REPL + headless agent. The flagship. | Individual devs doing interactive work; the thing you'll demo most. |
| **Factory App** | Desktop app connecting Droid to your local machine (incl. **Droid Control** for browser/desktop automation). | Local dev + QA/validation that needs to drive a real UI. |
| **Droid Exec** | Non-interactive, scriptable Droid (`droid exec`). | CI/CD, cron jobs, pre-commit hooks, automation pipelines. |
| **Web App** | Browser surface for Missions, Automations, Agent Readiness dashboards, Software Factory, Factory Router. | Team collaboration, async/long-running work, org-level visibility. |

Plus **IDE integrations** (VS Code, JetBrains, Zed) so the Droid shows up in the editor too.

**SE talking point:** the surfaces share one config/policy/context layer. A dev's AGENTS.md
conventions and the org's autonomy + model policy follow the Droid from CLI → CI → web.
That continuity is the differentiator vs. point tools.

## Core capabilities (the feature map)

- **Missions** — structured, multi-step, multi-agent execution (worker + validator). For
  large features and migrations.
- **Code Review** — `/review` analyzes uncommitted changes, PRs, or commits against reusable
  guidance (security, performance, standards).
- **Droid Control** — desktop/browser automation for QA and validation.
- **Agent Readiness** — measures how prepared a repo/org is for agentic work and tracks
  progress. *(This is a fantastic SE wedge — see note 05.)*
- **Cloud Templates / Computers** — preconfigured/cloud dev environments the Droid can run in.
- **AutoWiki** — auto-generated docs/wiki of a codebase.
- **Automations** — CI workflows, repo scanning, PR management from the web app.

## The concepts that power it (preview — detailed in later notes)

- **AGENTS.md** — the standard context file that teaches Droid your project conventions. (→ note 03)
- **Autonomy levels** — `default / low / medium / high` permission tiers. (→ note 02)
- **Spec Mode** — plan the work as a reviewable spec before executing. (→ note 04)
- **Model-agnostic / BYOK** — bring your own keys: Anthropic, OpenAI, Gemini, Groq,
  Fireworks, Baseten, DeepInfra, Hugging Face, OpenRouter, Ollama, LM Studio. (→ note 05)
- **Factory Router** — routes requests to models/gateways under org policy. (→ note 05)

## How a new user gets started (the happy path)

1. Install the CLI (`curl -fsSL https://app.factory.ai/cli | sh`) and run `droid` in a repo.
2. Let it explore the codebase; ask it to **"understand this project."**
3. Create an **AGENTS.md** (or have Droid draft one) so it learns your conventions.
4. Start in low autonomy; give it a small bug fix; review the diff; escalate trust.
5. Graduate to **Spec Mode** for a real feature, **Missions** for something big, and
   **`droid exec`** to wire it into CI.

## Self-check (Level 100 → ready for 200)

- [ ] I can name the four surfaces and what each is for.
- [ ] I can state the thesis ("model is table stakes, platform is the product") in one breath.
- [ ] I can explain task-delegation vs. autocomplete to a non-technical buyer.
- [ ] I installed the CLI and ran "understand this project" against a real repo.

Sources: [docs.factory.ai/welcome](https://docs.factory.ai/welcome) ·
[Product: CLI](https://factory.ai/product/cli) ·
[Common use cases](https://docs.factory.ai/cli/getting-started/common-use-cases)
