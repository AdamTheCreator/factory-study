# Spec Mode starting prompt

> Paste everything below the line into Droid **Spec Mode** (`droid --use-spec`, or
> Shift+Tab to the spec/plan mode) as your opening message, after AGENTS.md exists.
> Review the spec Droid produces, edit it visibly (cut scope, tighten acceptance
> criteria), then approve execution. The saved spec in `.factory/docs/` is a demo
> artifact — don't skip the review step.

---

Build **Triage Deck**, an internal incident-triage and status tool for BrightLedger, a
fintech company. The users are on-call engineers and engineering managers. The problem:
when an incident fires, the on-call engineer burns 20–30 minutes figuring out which
service is affected, which team owns it, which runbook applies, and what to tell the
business. This tool makes triage a 30-second read.

## Tech constraints

- Python 3.11+, FastAPI + uvicorn. Frontend: server-rendered Jinja2 templates plus a
  small amount of vanilla JS (fetch + DOM updates). No React, no build step, no database
  — all state is loaded from the JSON seed files into memory at startup; mutations
  (acknowledge/resolve) are in-memory only.
- No external network calls, no auth, no Docker. `pip install -r requirements.txt &&
  uvicorn app.main:app` must be the entire setup.
- pytest for tests. Keep dependencies to: fastapi, uvicorn, jinja2, pytest, httpx (for
  test client).

## Repository layout

```
triage-deck/
├── AGENTS.md                      # already present — follow it
├── README.md                      # quickstart + screenshots section
├── requirements.txt
├── data/
│   ├── incidents.json             # PagerDuty-shaped incidents (see schema below)
│   ├── alerts.json                # Datadog-shaped alerts
│   ├── teams.json                 # service → team routing metadata
│   └── runbooks/                  # one markdown runbook per service
├── services/                      # fake monorepo layer the tool routes against
│   ├── CODEOWNERS
│   ├── payments-api/              # each: main.py stub + brief README
│   ├── ledger-worker/
│   ├── notifications/
│   ├── auth-gateway/
│   └── risk-engine/
├── app/
│   ├── main.py                    # FastAPI app + routes
│   ├── models.py                  # pydantic models for incidents/alerts/teams
│   ├── triage.py                  # correlation, routing, suspected-upstream logic
│   ├── rca.py                     # RCA draft generator (template-based)
│   ├── templates/                 # Jinja2: board, incident detail, status page
│   └── static/                    # one stylesheet, one small JS file
└── tests/
    ├── test_triage.py
    └── test_api.py
```

## Milestone 1 — Data layer & fake monorepo

1. Generate the seed data exactly to the schemas in `seed-data-schema.md` (in my repo —
   I will paste the schemas as a follow-up if you need them): 14 incidents spread over
   the last 7 days across the 5 services (statuses: mostly resolved, 2 acknowledged,
   2 triggered), ~30 alerts referenced by those incidents, and a `teams.json` covering
   all 5 services.
2. **Demo-critical:** exactly one incident must be a `triggered`, unacknowledged
   **SEV-1 on payments-api** created "minutes ago", whose alerts include a log sample
   implicating `ledger-worker` as the upstream cause
   (`ConnectionPoolTimeout: ledger-worker grpc upstream timed out`).
3. Create the 5 service stubs under `services/` (a plausible ~50-line FastAPI/worker
   `main.py` each + README) and a `CODEOWNERS` mapping each service dir to its team.
4. Write one runbook per service in `data/runbooks/` (real structure: symptoms, checks,
   escalation, rollback), each ~30 lines.

## Milestone 2 — Triage engine + tests

`app/triage.py` must, deterministically (no LLM calls):

1. Correlate alerts to incidents via `alert_ids` and `service` tags.
2. Route each incident: service → owning team, Slack channel, escalation contact
   (from `teams.json`, cross-checked against CODEOWNERS).
3. Extract **suspected upstream service** from alert `log_sample` strings by matching
   known service names — e.g. the SEV-1 on payments-api should surface
   "suspected upstream: ledger-worker".
4. Attach the matching runbook path and compute a **triage summary** per incident:
   one paragraph of plain English covering severity, customer impact, owner, suspected
   cause, next step. Assemble it from the structured fields (template, not AI).
5. Compute per-service **component status** for the status page: `operational` /
   `degraded` (active SEV-3/4) / `major_outage` (active SEV-1/2).

Tests: routing correctness for every service, upstream extraction from log samples,
component-status derivation, and the ack/resolve state transitions.

## Milestone 3 — Web UI (three views)

1. **Triage board (`/`)** — active incidents sorted SEV-1 first, then by age. Each card:
   severity badge, title, service, owning team + Slack channel, suspected upstream,
   age, links to runbook and detail page, Acknowledge/Resolve buttons (POST, in-memory).
   Resolved incidents collapse into a history section below.
2. **Incident detail (`/incident/{id}`)** — triage summary paragraph, linked alerts with
   metric/threshold/value, timeline (alerts fired → triggered → acked → resolved),
   customer impact, runbook rendered inline, and a **"Draft RCA"** button that returns a
   pre-filled markdown RCA from `app/rca.py` (incident facts injected into a standard
   template: summary, timeline, root cause placeholder, action items).
3. **Status page (`/status`)** — customer-facing: component list with status pills and
   an overall banner. No internal details (no team names, no log samples).

Style: clean, dense, dark-friendly; system font stack; a single CSS file. It should look
like a credible internal tool, not a design showcase — do not spend effort on animations.

## Acceptance criteria

- `uvicorn app.main:app` serves all three views against the seed data with zero config.
- The seeded SEV-1 appears at the top of the board with team `payments`, channel
  `#oncall-payments`, suspected upstream `ledger-worker`, and its runbook linked.
- Acknowledging it via the UI moves it to acknowledged and the status page shows
  payments as `major_outage` while active, `operational` once resolved.
- `pytest` passes; triage logic has meaningful coverage, not smoke tests.
- README documents setup in ≤5 lines.

## Out of scope (do not build)

Auth, persistence, real PagerDuty/Datadog integrations, websockets/live updates, LLM
summarization (stretch only, behind an env flag, after everything above is done),
deployment config.
