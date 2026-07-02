# 06 — Competitive Landscape

In an SE interview you *will* get "how is this different from ___?" Answer honestly and
crisply — overclaiming kills credibility with technical buyers. The frame that wins:
**category, not feature checklist.**

## The category map

| Tool | What it fundamentally is | Primary surface |
|------|--------------------------|-----------------|
| **Factory (Droid)** | AI-native **dev platform** — same agent across CLI/IDE/CI/Web, model-agnostic, enterprise governance | Everywhere (terminal, IDE, headless, web) |
| **Cursor** | AI-first **code editor** (VS Code fork) | The editor |
| **Claude Code** | Anthropic's **terminal coding agent** | Terminal (Anthropic models) |
| **GitHub Copilot** | **Autocomplete + chat** in the editor/PRs | Editor / GitHub |
| **Devin (Cognition)** | Autonomous agent in its **own sandbox** (browser+terminal+editor), task via Slack/web | Hosted sandbox |

## One-liners (memorize)

- **vs. Cursor:** *"Cursor is an editor; Factory is a platform. Cursor is great when work
  happens in the editor. Factory is the same Droid + your conventions + your org policy
  following you from laptop to CI to web — and it's model-agnostic, not tied to one editor."*
- **vs. Claude Code:** *"Closest in feel — both are terminal-first agents (we deliberately
  match the UX). Difference is the platform around it: model-agnostic BYOK/Router, IDE + web +
  headless surfaces, Missions, enterprise governance (SSO, audit, hierarchical policy), Agent
  Readiness. Claude Code is excellent and Anthropic-model-centric; Factory is the org layer."*
- **vs. Copilot:** *"Copilot autocompletes inside the editor; Factory delegates whole tasks
  across surfaces. Different altitude — suggestions vs. shipped units of work. Many teams keep
  Copilot for inline and add Factory for delegation."*
- **vs. Devin:** *"Both do autonomous task delegation. Devin lives in its own hosted sandbox;
  Factory meets you in *your* environment (your terminal, IDE, CI, machine via the app) with
  granular autonomy tiers and BYOK. Control and integration vs. fully-hosted black box."*

## Where Factory genuinely wins (lead with these)

1. **Surface-agnostic continuity** — one agent + one config/policy/context layer across
   CLI, IDE, headless, web. Competitors are mostly single-surface.
2. **Model independence (BYOK + Router)** — no lab lock-in; route per task; use your own
   contracts/gateways; self-host open models (incl. **Baseten** — your wheelhouse).
3. **Enterprise governance depth** — autonomy tiers, SSO/SCIM, audit, hierarchical
   extension-only settings, EU deploy, telemetry export. Built for security review.
4. **Workflow breadth** — Spec Mode, Missions (worker/validator), Droid Exec, `/review`,
   Droid Control, Agent Readiness — a lifecycle, not a single trick.
5. **Agent Readiness** — nobody else frames adoption as a measurable maturity program.

## Be honest about where others are strong (credibility)

- **Cursor** has a beloved in-editor UX and huge mindshare; if a team lives in the editor and
  wants tab-completion + inline chat, that's its home turf.
- **Claude Code** is excellent and simple if you're all-in on Anthropic models and terminal.
- **Copilot** has unmatched distribution and GitHub-native integration; low-friction default.
- **Devin** appeals when teams want a fully-hosted "fire-and-forget" agent and don't want to
  manage environments.

Coexistence is fine and common: *"You can keep Copilot for inline and bring Factory for
delegation + governance."* Don't force a rip-and-replace; that's not how technical buyers move.

## The trap to avoid

Don't get dragged into a benchmark/feature-checklist slugfest. Pull up to **category and
operating model**: *"The question isn't whose autocomplete is 3% better. It's: do you want a
single governed agent across your whole SDLC, on the models you choose? That's the Factory bet."*

## Pricing posture (directional — verify live)

Factory uses **token/usage-based billing** (via Orb) rather than pure per-seat — free tier to
pro (~$20/mo range) up through enterprise (custom, with dedicated compute, SSO, support).
Token-based billing ties cost to value delivered and avoids paying for idle seats. **Numbers
shift — always confirm at [factory.ai/pricing](https://factory.ai/pricing) before quoting.**

Reference points: Devin ≈ $20 base + ~$2.25/ACU (≈15 min work); Cursor team ≈ $40/user;
Claude Code via Claude Pro ≈ $20/mo or API usage.

## Self-check (Level 300)
- [ ] I can give the four one-liners (Cursor/Claude Code/Copilot/Devin) without notes.
- [ ] I can concede each competitor's real strength credibly.
- [ ] I can pull a feature-checklist debate up to category/operating-model.
- [ ] I can explain token-based billing vs. per-seat and why it can favor the customer.

Sources: [Factory pricing](https://factory.ai/pricing) ·
[Orb case study](https://www.withorb.com/case-studies/factory) ·
[Claude Code vs Cursor vs Devin (2026)](https://cowork.ink/blog/claude-code-vs-cursor-vs-devin-vs-windsurf/)
