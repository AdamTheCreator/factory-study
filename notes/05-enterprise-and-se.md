# 05 — Enterprise Features & the SE Lens

This is the note that turns "I can use Droid" into "I can sell and deploy Droid at a
company." The SE role lives here. Two halves: **(A) the enterprise feature surface** you must
be able to speak to, and **(B) the SE motion** — discovery, demo, POC, objections, ROI.

---

## A. Enterprise feature surface

### Model independence — BYOK, Router & Gateways
- **BYOK (Bring Your Own Key):** route to Anthropic, OpenAI, Gemini, Groq, Fireworks,
  **Baseten**, DeepInfra, Hugging Face, OpenRouter — and **local** models via Ollama / LM Studio.
- **Mixed models:** different models for different jobs (e.g., strong model for spec planning,
  cheaper for execution; `--spec-model`).
- **Factory Router / models & gateways:** centrally route requests to approved models/gateways
  under org policy. Customers keep data on their own model contracts and control spend/routing.

> SE gold: *"You're not locked to one lab. Use your existing model contracts, route by task,
> swap models as the frontier moves — without changing your devs' workflow."* Note the
> **Baseten** connection — your inference-engineering background (this repo!) is directly
> relevant when a customer self-hosts open models behind Factory.

### Security & autonomy governance
- **Autonomy levels** (note 02) as org policy — cap what Droid can do per environment.
- **Droid Shield / Shield Plus** — account/CLI security controls.
- **LLM safety**, **security review**, **GitHub security** — guardrails around what the agent
  touches and what leaves the building.

### Identity, access & governance
- **SSO / SAML / SCIM** — enterprise auth & user provisioning.
- **Hierarchical settings** — Organization → Project → User, with **extension-only** semantics
  (lower levels add to, can't silently undermine, org policy). Know this phrase.
- **Service accounts** — API keys for automation, with rotation/revocation.
- **Compliance & audit**, **telemetry export**, **usage analytics** — visibility for security
  and finance.

### Deployment & data flows
- **EU deployment**, **network configuration**, **privacy & data flows**, **VPS deployment**.
- **Computers / Cloud Templates** — managed/preconfigured environments the Droid runs in.
- **Plugin registry** — curated internal plugins for the org.

### Agent Readiness (your favorite wedge)
A score + dashboard measuring how prepared a repo/org is for agentic development (conventions
documented? tests reliable? CI clean? AGENTS.md present?) and tracking progress over time.

**Why it's an SE superpower:** it reframes the sale from "buy a tool" to "here's a maturity
roadmap." You can run a readiness assessment in discovery, expose concrete gaps, and tie
adoption to closing them. It also creates natural expansion (low score → services + seats).

---

## B. The SE motion (Factory edition)

Mirror your Baseten POC playbook, adapted to agentic dev tooling.

### 1. Discovery — questions that matter
- Where do your engineers lose time? (boilerplate, migrations, reviews, on-call toil)
- What's your model situation — single vendor, multi, self-hosted? (sets up BYOK/Router)
- How do you feel about autonomy? What would a security review require? (sets up autonomy tiers, audit, SSO)
- What does "done" look like — IDE productivity, or CI/automation at team scale?
- How healthy are your repos? (tees up **Agent Readiness**)

### 2. The demo arc (15–20 min, do-don't-tell)
1. **Ground it:** open a real-ish repo, show/draft **AGENTS.md**, run `/context`. ("Most agent
   failures are context failures — here's how we fix that.")
2. **Small win, controlled:** fix a bug at `--auto low`, review the diff. Show the autonomy dial.
3. **Plan a real feature:** **Spec Mode** → show the reviewable spec in `.factory/docs/`. (Trust.)
4. **Go big:** kick a **Mission** (worker/validator) on a larger task. (Scale.)
5. **Make it infrastructure:** show **`droid exec`** in a GitHub Action. (Team leverage.)
6. **Close the loop:** **`/review`** on the changes; mention Droid Control for UI QA.
7. **Zoom out:** **Agent Readiness** dashboard + enterprise governance (SSO, audit, Router).

> Demo discipline: never run `--skip-permissions-unsafe` on anything real; start low and
> escalate; let the customer drive a step themselves — hands on keyboard converts.

### 3. POC / "land" criteria
Define success up front with the champion. Good metrics:
- Cycle-time on a class of task (e.g., median PR time for X work) — before/after.
- % of PRs getting an automated first-pass review.
- On-call/incident toil reduced.
- Agent Readiness score improvement.
Set a 2–4 week window, a named champion, a target repo, and a written success definition.

### 4. Objection handling (have crisp answers — full set in note 06)
- *"How is this different from Cursor?"* → Surface-agnostic + agent-first + governance, not an editor. (note 06)
- *"We already use Copilot."* → Copilot autocompletes; Factory delegates whole tasks across surfaces.
- *"Security won't allow an autonomous agent."* → Autonomy tiers, Spec Mode review, audit, SSO,
  EU deploy, BYOK keeps data on your contracts.
- *"Model lock-in scares us."* → Model-agnostic by design; bring your own keys/gateways.
- *"Our codebase is huge/messy."* → Context compression + AGENTS.md + Agent Readiness roadmap.
- *"Will it hallucinate and break prod?"* → Default is read-only; you choose autonomy; Missions
  add a validator; everything's reviewable.

### 5. ROI framing
- **Time saved** × loaded eng cost on delegated task classes.
- **Quality**: fewer escaped defects via automated review/validation.
- **Throughput**: parallel agents (Missions, exec in CI) vs. linear human work.
- **Risk reduced**: standardized review, audit trail, governed autonomy.
- Token-based billing → tie spend to value delivered, not idle seats (use `/cost`, usage analytics).

---

## Hands-on rep (Level 300/400 prep)
1. Configure **BYOK** with at least one provider key on your trial; switch models mid-session.
2. Run an **Agent Readiness** report on a repo and write the 3 gaps you'd raise in discovery.
3. Build and rehearse the **7-step demo arc** end to end, out loud, under 20 minutes.
4. Draft a one-page **POC success plan** for an imaginary customer.

## Self-check (Level 300)
- [ ] I can explain BYOK/Router and why model-independence matters to a buyer.
- [ ] I can name the governance features a security review will ask about (SSO/SCIM, audit, autonomy, hierarchical settings, EU/network, data flows).
- [ ] I can run the demo arc cold and adapt it on the fly.
- [ ] I can pitch Agent Readiness as a roadmap, not just a score.

Sources: [Enterprise docs](https://docs.factory.ai/user-guides/enterprise/overview) ·
[Hierarchical settings](https://docs.factory.ai/user-guides/enterprise/hierarchical-settings) ·
[BYOK](https://docs.factory.ai/cli/byok/overview) ·
[Models & gateways](https://docs.factory.ai/user-guides/enterprise/models-and-gateways) ·
[Agent readiness](https://docs.factory.ai/web/agent-readiness/overview)
