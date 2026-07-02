# 08 — Glossary & Interview Prep

## Glossary (say these naturally)

| Term | Meaning |
|------|---------|
| **Droid** | Factory's AI agent. The thing that does the work. |
| **Droid CLI** | Terminal REPL + headless agent; the flagship surface. |
| **Droid Exec** | Headless, non-interactive Droid (`droid exec`) for CI/automation. |
| **Droid Control** | Desktop/browser automation for QA and validation. |
| **Factory App** | Desktop app linking Droid to your local machine. |
| **Web App** | Browser surface: Missions, Automations, Agent Readiness, Software Factory, Router. |
| **AGENTS.md** | Open-standard context file teaching the agent your repo's conventions. |
| **Autonomy levels** | `default/low/medium/high` (+ unsafe) — what Droid may do without asking. |
| **Spec Mode** | Plan the work as a reviewable spec before executing (`--use-spec`); saved in `.factory/docs/`. |
| **Mission Mode** | Multi-agent execution (worker + validator) for large work. |
| **Skills** | Reusable agent capabilities (`/skills`). |
| **Custom Droids** | Specialized agents you define for recurring workflows. |
| **MCP** | Model Context Protocol — standard way to connect external tools/data sources. |
| **BYOK** | Bring Your Own Key — use your own model-provider keys. |
| **Factory Router** | Routes requests to approved models/gateways under org policy. |
| **Mixed models** | Different models for different jobs (e.g., `--spec-model`). |
| **Hierarchical settings** | Org → Project → User config, **extension-only** semantics. |
| **Droid Shield / Shield Plus** | Account/CLI security controls. |
| **Agent Readiness** | Score + dashboard for how prepared a repo/org is for agentic dev. |
| **AutoWiki** | Auto-generated, maintained codebase wiki/docs. |
| **Automations** | Web-app CI workflows, repo scanning, PR management. |
| **Computers / Cloud Templates** | Managed/preconfigured environments Droid can run in. |
| **Context compression** | Keeping high-confidence anchors + compressing the rest to scale to big codebases. |
| **Organizational memory** | Persistent team conventions across sessions. |

## Likely interview questions (and how to answer)

**"What is Factory, in one sentence?"**
> An AI-native software development platform: you delegate complete engineering tasks to a
> Droid that works across your terminal, IDE, CI, and the web — model-agnostic, with
> enterprise governance.

**"Walk me through how you'd onboard a new customer team."**
> Discovery (pain, model stance, security bar, repo health) → write/generate an AGENTS.md and
> show grounding via `/context` → small controlled win at low autonomy → Spec Mode on a real
> feature → a Mission on something bigger → wire `droid exec` into their CI → stand up `/review`
> automation → run an Agent Readiness report and turn the gaps into a 2–4 week POC plan with
> named success metrics and a champion.

**"How is this different from Cursor / Copilot / Devin / Claude Code?"**
> Category, not checklist. (Use the four one-liners from note 06.) Concede their real
> strengths; lead with surface-continuity, model-independence, governance, workflow breadth.

**"A security lead says 'no autonomous agents on our repos.' What do you do?"**
> Meet the objection on their terms: default is read-only; autonomy is a dial they set per
> environment; Spec Mode keeps humans in control at design time; Missions add a validator;
> everything's reviewable; plus SSO/SCIM, audit, telemetry export, EU deployment, and BYOK so
> data stays on their model contracts. Then propose a low-autonomy, single-repo POC to build trust.

**"How would you handle a failing/low-value POC?"**
> Re-anchor on the success criteria we set, diagnose whether it's a context problem (usually
> AGENTS.md / integrations), a scope problem (wrong task class), or a fit problem (be honest).
> Adjust one variable, re-measure. Don't let a POC drift without a defined finish line.

**"Where does Factory NOT fit?"**
> If a team purely wants in-editor autocomplete and nothing else, Copilot/Cursor may suffice.
> If they refuse any environment integration and want a fully-hosted black box, Devin's model
> differs. Honesty here builds trust — and most teams can coexist (keep inline tools, add
> Factory for delegation + governance).

**"Your background is inference/Baseten — why does that help here?"**
> Two ways: (1) I can speak credibly to the **model layer** — BYOK, self-hosting open models,
> cost/latency tradeoffs, routing — which matters for Factory's model-agnostic story (Baseten
> is even a supported BYOK provider). (2) I've already run **POCs that prove value with
> metrics**, which is the core SE loop here too.

## Crisp talking points (sound bites)
- "The model is table stakes; the platform around it is the product."
- "Most agent failures are context failures — we fix that with AGENTS.md, integrations, and memory."
- "Autonomy is a dial, not a switch — that's how you make agents acceptable to security."
- "One governed agent across your whole SDLC, on the models you choose."
- "We don't rip and replace — keep your inline tools, add Factory for delegation."
- "Adoption is a maturity program, not a download — that's what Agent Readiness measures."

## Final gut-check before the interview
- [ ] I can give the 2-min pitch and the 20-min demo cold.
- [ ] I can answer the 7 questions above without notes.
- [ ] I have artifacts to screen-share (AGENTS.md, Mission, CI integration, demo).
- [ ] I confirmed pricing/feature specifics against the live docs *today*.
- [ ] I can connect my Baseten/inference background to Factory's model-agnostic story.

Sources: [How to talk to Droids](https://docs.factory.ai/cli/getting-started/how-to-talk-to-droids) ·
[Overview](https://docs.factory.ai/welcome) ·
[Available models](https://docs.factory.ai/reference/available-models)
