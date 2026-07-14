# Seed data schemas — Triage Deck

Shaped like PagerDuty (incidents) and Datadog (alerts) payloads so the demo line lands:
*"in production this is the PagerDuty webhook and Datadog monitors; for the demo it's
seeded data."* They are simplified, not exact vendor schemas — say "shaped like," don't
claim API fidelity if a panelist knows the real payloads.

## `data/incidents.json` — PagerDuty-shaped

```json
{
  "id": "INC-1042",
  "title": "Elevated 5xx and p99 latency on payments-api",
  "status": "triggered",
  "urgency": "high",
  "severity": "SEV-1",
  "service": "payments-api",
  "created_at": "2026-07-14T14:22:31Z",
  "acknowledged_at": null,
  "resolved_at": null,
  "assignee": null,
  "alert_ids": ["DD-88121", "DD-88123"],
  "customer_impact": "Card advance disbursements failing for ~8% of requests"
}
```

Field notes:
- `status`: `triggered` | `acknowledged` | `resolved`. Timestamps null until reached.
- `severity`: `SEV-1` (customer-facing outage) → `SEV-4` (minor/internal).
- `service`: must match a directory name under `services/` — this is the routing key.
- `alert_ids`: joins to `alerts.json`.
- `assignee`: engineer name once acknowledged, else null.

Distribution for the 14 seeded incidents:
- **1 × SEV-1 `triggered` on payments-api, created minutes ago, unassigned** — the demo
  centerpiece. Its alerts must implicate ledger-worker (see alert DD-88121 below).
- 1 × SEV-3 `triggered` (notifications — e.g. webhook delivery lag), low urgency.
- 2 × `acknowledged` (SEV-2 auth-gateway, SEV-3 risk-engine), assigned, 1–4 hours old.
- 10 × `resolved`, spread over the past 7 days across all services, varied severities —
  enough history to make the board and status page look lived-in.

## `data/alerts.json` — Datadog-shaped

```json
{
  "id": "DD-88121",
  "monitor_name": "payments-api p99 request latency",
  "alert_type": "metric",
  "metric": "trace.fastapi.request.duration.p99",
  "threshold": 1.5,
  "value": 4.8,
  "unit": "s",
  "tags": ["service:payments-api", "env:prod", "team:payments"],
  "triggered_at": "2026-07-14T14:20:05Z",
  "log_sample": "ConnectionPoolTimeout: ledger-worker grpc upstream timed out after 3000ms"
}
```

Field notes:
- `alert_type`: `metric` | `log` | `apm`.
- `tags`: always include `service:<name>` and `env:prod` — the correlation keys.
- `log_sample`: one representative log line; **this is where the suspected-upstream
  story lives.** For the SEV-1's alerts, the log samples must name `ledger-worker` so
  the triage engine can surface "suspected upstream: ledger-worker". Give 2–3 other
  incidents cross-service log samples too (e.g. risk-engine timing out on auth-gateway)
  so the feature doesn't look hard-coded to one row.
- ~30 alerts total; every incident's `alert_ids` must resolve; a couple of alerts can
  share an incident (alert storm → one incident is itself a triage talking point).

## `data/teams.json` — routing metadata

```json
{
  "payments": {
    "owns": ["payments-api", "ledger-worker"],
    "slack_channel": "#oncall-payments",
    "escalation": "Priya N. (EM)",
    "pagerduty_schedule": "payments-primary"
  }
}
```

Five services, four teams (payments owns two services — makes routing non-trivial):
- **payments** → payments-api, ledger-worker
- **identity** → auth-gateway
- **risk** → risk-engine
- **comms** → notifications

`services/CODEOWNERS` must agree with this file
(`/services/payments-api/ @brightledger/payments` etc.) — the triage engine cross-checks
them, and "the tool reads the same CODEOWNERS your repo already has" is a demo line.

## `data/runbooks/<service>.md`

One per service, ~30 lines, real structure:

```markdown
# Runbook — payments-api

## Symptoms
- p99 > 1.5s, elevated 5xx on /disburse

## First checks
1. ledger-worker gRPC health: `grpcurl ... list`
2. Connection pool saturation dashboard: <link>

## Escalation
- #oncall-payments → Priya N. (EM)

## Rollback
- `deployctl rollback payments-api --to-previous`
```

The payments-api runbook's "first checks" should point at ledger-worker — so in the
demo, the suspected-upstream field and the runbook agree, and the story closes: alert →
incident → owner → cause → runbook → action.
