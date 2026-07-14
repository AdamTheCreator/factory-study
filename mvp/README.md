# MVP — "Triage Deck" (Factory SE Interview Project)

The interview project for Parts #1 and #2: an **incident triage & status tool** for a
fictional fintech, built entirely with Factory (Droid) in a ≤4-hour timebox.

## The scenario (memorize this framing)

- **Fictional customer:** *BrightLedger* — a fintech processing card advances and
  credit-building payments. ~200 engineers across 6 pods, on-call rotation per pod.
  Modeled on Factory's real [Empower case study](https://factory.ai/case-studies/empower)
  (fintech, 40% faster incident response, 50% faster PR approval) so every claim in the
  demo has a public proof point behind it.
- **Persona:** Head of Developer Productivity (panel roles: VP Eng, EM of Payments pod).
- **Pain:** on-call engineers lose the first 20–30 minutes of every incident to triage —
  which service, which team owns it, which runbook, what to tell the business. Runbooks
  are stale; status comms are manual. *"Almost 100% of engineers will tell you they're at
  least slightly nervous when on call."* — staff engineer quote from the Empower study.
  Open the Part 2 pitch with it.
- **Competitive backdrop (Part 2):** BrightLedger is already rolling out Claude Code to
  ICs and has a platform team debating building internal agent tooling. They self-host
  open models (via Baseten) for cost/data reasons → BYOK/Router is the wedge.
- **The MVP:** **Triage Deck** — ingests PagerDuty-shaped incidents + Datadog-shaped
  alerts, routes each incident to its owning team via the service catalog/CODEOWNERS,
  surfaces the right runbook and suspected upstream cause, and renders a triage board +
  customer-facing status page + one-click RCA draft.
- **The two-layer demo:** Layer 1 is the tool. Layer 2 — the real product — is *how it
  was built*: AGENTS.md, the Spec Mode spec, session history, `/review` findings,
  `/cost`. "Your team ships internal tools like this in an afternoon, governed, on your
  models."

## Files here

- **[spec-prompt.md](spec-prompt.md)** — the exact prompt to paste into Droid Spec Mode
  (`--use-spec`) as your opening move. Contains the repo skeleton, milestones, and
  acceptance criteria.
- **[seed-data-schema.md](seed-data-schema.md)** — schemas + sample records for the
  incident/alert/team seed data, shaped like PagerDuty & Datadog payloads.

## 4-hour run of show

| Clock | Do | Receipt to capture |
|-------|----|--------------------|
| 0:00–0:20 | New repo (`triage-deck`). Write AGENTS.md from `templates/AGENTS.md`. Run `droid`, "understand this project". | Screenshot `/context` before vs. after AGENTS.md. |
| 0:20–0:50 | Paste **spec-prompt.md** into Spec Mode. Review and *edit* the spec it produces (show judgment, don't rubber-stamp). | The saved spec in `.factory/docs/`. |
| 0:50–1:30 | Execute Milestone 1 (seed data + services layer + models) at `--auto low`. Review diffs. | Note one place you corrected Droid. |
| 1:30–2:45 | Milestones 2–3 (triage engine + tests, then dashboard) at medium/high autonomy. | Session IDs — `/rename` + `/favorite` them. |
| 2:45–3:15 | `/review` the whole build; have Droid fix its own findings. Stretch: `droid exec` GitHub Action that runs `/review` on PRs. | `/review` output; the Action YAML. |
| 3:15–4:00 | Rehearse the walkthrough. Run `/cost` and write the number down. | "$X of tokens for a tool that saves 20 min per incident." |

## Demo beats (Part 1 walkthrough order)

1. Open the **triage board** — one SEV-1 sits un-acknowledged at the top (seeded that way
   on purpose). Walk it: severity, owning team, Slack channel, suspected upstream
   (ledger-worker, extracted from the alert's log sample), linked runbook.
2. Acknowledge it live → **status page** flips the Payments component to *degraded*.
3. Click **Draft RCA** → markdown RCA skeleton pre-filled from the timeline.
4. Then the turn: "Now let me show you how this got built" → spec file, AGENTS.md,
   session history, `/review`, `/cost`. That's the Factory sale.

## Guardrails

- Build **through Factory only** — the session history in your account is part of the
  evaluation. No side-channel coding.
- Don't gold-plate the UI. Functionality > polish per the brief; spend surplus time on
  the talk track, not CSS.
- Never demo with `--skip-permissions-unsafe`. Start low autonomy, escalate on camera —
  the autonomy dial *is* a talking point.
