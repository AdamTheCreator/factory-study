# Factory.ai — Solutions Engineer Study Guide (Level 100 → 300)

> Prepping for the **Solutions Engineer (SE)** role at Factory.
> Goal: go from "never opened it" to **Level 300** — an advanced practitioner who can
> drive Droid live, design an adoption rollout, handle objections, and demo the
> platform to a skeptical engineering team without notes.
>
> *Mirrors the structure of the Baseten study guide in the repo root, but tuned for
> the SE motion: discovery → demo → POC → rollout → expansion.*

## What "Level 300" means here

| Level | You can... |
|-------|-----------|
| **100** | Explain what Factory is, name the surfaces (CLI / IDE / Exec / Web), install Droid, run a basic prompt. |
| **200** | Drive the Droid CLI fluently — modes, autonomy levels, AGENTS.md, spec mode, slash commands. Write a clean AGENTS.md for a repo. |
| **300** | Run `droid exec` headless in CI, orchestrate Missions, wire MCP + integrations, configure enterprise settings (BYOK, gateways, SSO, hierarchical config), **and** map all of it to a customer's workflow in a live demo. Handle "why not Cursor/Devin/Claude Code?" cold. |
| **400** (bonus) | Build custom Droids/plugins, design org-wide rollout + Agent Readiness program, integrate with a customer's stack end to end. |

## How to use this guide

Work the notes in order, but **the trial is the real teacher** — every note ends with a
hands-on rep you run against a real repo. SE interviews reward *show, don't tell*.

1. **[01 — What Factory Is](notes/01-what-is-factory.md)** — The product, the four surfaces, the "AI-native dev platform" thesis, and why it exists. Positioning vs. the category.
2. **[02 — Droid CLI Deep Dive](notes/02-droid-cli.md)** — Commands, slash commands, modes, autonomy levels, keyboard shortcuts, sessions. Your bread and butter.
3. **[03 — Context, AGENTS.md & Memory](notes/03-context-and-agents.md)** — How Droid stays grounded: AGENTS.md, context compression, organizational memory, rules/conventions. The #1 thing that separates good from bad outcomes.
4. **[04 — Workflows: Spec, Missions, Exec, Review](notes/04-workflows.md)** — Spec mode, Mission Mode (multi-agent), headless `droid exec`, `/review`, Droid Control. The capabilities you'll demo.
5. **[05 — Enterprise & the SE Lens](notes/05-enterprise-and-se.md)** — BYOK, Factory Router/gateways, SSO/SCIM, hierarchical settings, Droid Shield, Agent Readiness. Plus the SE motion: discovery, demo script, POC, objection handling, ROI.
6. **[06 — Competitive Landscape](notes/06-competitive.md)** — Factory vs. Cursor, Devin, Claude Code, Copilot. Where Factory wins, where it doesn't, and how to talk about it honestly.
7. **[07 — The 30-Day Trial Plan](notes/07-hands-on-plan.md)** — A day-by-day plan to burn down your trial and hit Level 300 with proof you can show in the interview.
8. **[08 — Glossary & Interview Prep](notes/08-glossary-interview.md)** — Terminology, likely interview questions, and crisp talking points.

## Practice artifacts

- **[templates/AGENTS.md](templates/AGENTS.md)** — a ready-to-fill AGENTS.md for your sandbox/demo repo, with a "why each section exists" key.
- **[demo/demo-script.md](demo/demo-script.md)** — the 7-step demo arc as a rehearsable 20-minute script, with an interruption playbook.
- **[drills/mock-interview.md](drills/mock-interview.md)** — 30 questions + 5 roleplays, scored the same way as the Baseten quiz bank.

## TL;DR for the impatient (read this, then start the trial)

**What it is:** Factory is an *AI-native software development platform*. Its agent is the
**Droid**, which runs **everywhere you work** — terminal (Droid CLI), IDE (VS Code/JetBrains/Zed),
headless (`droid exec` in CI/CD), and the Web app. You delegate whole tasks (refactors,
migrations, incident response, code review) rather than autocompleting lines.

**Why it's different from Cursor:** Cursor is an *editor*. Factory is *surface-agnostic* and
agent-first — the same Droid, your conventions (AGENTS.md), and your org policy follow you
from laptop to CI to web. It's **model-agnostic** (BYOK: Anthropic, OpenAI, Gemini, open models)
and built for **enterprise governance** (SSO, audit, gateways, autonomy tiers).

**The killer concepts to memorize:**
- **AGENTS.md** — the standard file that teaches Droid your repo's conventions.
- **Autonomy levels** (`--auto low/medium/high`) — how much Droid can do without asking.
- **Spec Mode** (`--use-spec`) — plan-as-a-spec before executing.
- **Missions** — multi-agent (worker + validator) execution for large work.
- **Droid Exec** — headless/scriptable Droid for CI and automation.
- **Agent Readiness** — a score for how prepared a repo/org is for agents (great SE wedge).

> ⚠️ **Accuracy note:** Pricing and exact feature tiers change fast. Everything here was
> compiled from public docs (docs.factory.ai) as of mid-2026. Always confirm specifics
> against the live docs before quoting them to a customer — and use your trial to verify.

## Quick start (do this first)

```bash
# Install the Droid CLI
curl -fsSL https://app.factory.ai/cli | sh

# Drop into a real repo and launch the interactive REPL
cd your-project && droid

# Inside the REPL, the muscle memory to build:
#   Shift+Tab  → cycle modes (default → auto → plan/spec)
#   Ctrl+L     → cycle autonomy levels
#   Ctrl+N     → cycle models
#   /review    → review your uncommitted changes
#   /missions  → multi-agent mode for a big task
#   /context   → see what Droid is holding in context
```

Sources: [docs.factory.ai/welcome](https://docs.factory.ai/welcome) ·
[CLI reference](https://docs.factory.ai/reference/cli-reference) ·
[Sid Bharath's Factory guide](https://sidbharath.com/blog/factory-ai-guide/)
