# 07 — The 30-Day Trial Plan (→ Level 300)

You have a 30-day trial. **Reading gets you to ~150; reps get you to 300.** This is a
day-by-day plan that produces *artifacts you can show in the interview* ("here's a Mission I
ran, here's a CI integration I built, here's the demo I'd give you").

Pick **one real repo** to be your sandbox the whole time — ideally something non-trivial you
understand (a side project, or fork a popular OSS repo). Consistency compounds.

## Week 1 — Fluency (Level 100 → 200)

| Day | Do | Artifact |
|-----|----|----------|
| 1 | Install CLI; run `droid`; "understand this project"; explore `/help`, `/context`, `/status`. | Notes on what it loaded. |
| 2 | Practice the shortcut dance: Shift+Tab modes, Ctrl+L autonomy, Ctrl+N models, Tab effort. Fix a tiny bug at `--auto low`. | A reviewed diff. |
| 3 | Draft an **AGENTS.md** (have Droid draft, then you edit to high-signal). Re-run a task before/after it. | Committed AGENTS.md + before/after note. |
| 4 | Sessions: resume, fork, search. Run 2 tasks at different autonomy levels; note the difference. | Session log. |
| 5 | First **Spec Mode** run on a small feature; read the spec in `.factory/docs/`. | Saved spec. |
| 6 | `/review` on a messy branch; read findings. Try `/skills`. | Review output. |
| 7 | **Teach-back:** write a 1-paragraph "what Factory is" + record yourself giving the 2-min pitch. | Pitch recording/script. |

## Week 2 — Depth (Level 200 → 250)

| Day | Do | Artifact |
|-----|----|----------|
| 8–9 | **Missions**: run a larger feature/migration; watch worker/validator. Note where it helped/struggled. | Mission writeup. |
| 10 | **`droid exec`** headless: run a task, get `-o json`, parse it in a tiny script. | Working exec command. |
| 11 | Wire `droid exec` into a **GitHub Action** on a throwaway repo (e.g., auto-fix lint on PR). | Green CI run. |
| 12 | **BYOK**: add a provider key; switch models mid-session; try `--spec-model` (strong plan, cheap exec). | Config + cost comparison. |
| 13 | One **MCP/integration** (GitHub easiest): ask Droid about a real PR/issue. | Integrated session. |
| 14 | **Teach-back:** explain Spec vs. Missions vs. Exec and when to use each, out loud. | Decision cheat-sheet (your words). |

## Week 3 — The SE motion (Level 250 → 300)

| Day | Do | Artifact |
|-----|----|----------|
| 15 | Run an **Agent Readiness** report; write the 3 gaps you'd raise in discovery. | Readiness writeup. |
| 16 | Study enterprise surface (note 05): SSO/SCIM, audit, hierarchical settings, Router, EU/network. | Governance Q&A sheet. |
| 17 | Draft a **discovery question set** for a hypothetical customer (fintech? infra startup? enterprise?). | Discovery doc. |
| 18 | Build the **7-step demo arc** (note 05B). Script it. | Demo script. |
| 19 | **Rehearse the demo** end-to-end, under 20 min, on your sandbox repo. Record it. | Demo recording v1. |
| 20 | Write **objection-handling** answers (note 06) in your own words; rehearse the 4 competitor one-liners. | Objection cheat-sheet. |
| 21 | **Teach-back:** deliver the full demo to a friend/rubber-duck; note where you stumbled. | Demo recording v2. |

## Week 4 — Polish & proof (Level 300, interview-ready)

| Day | Do | Artifact |
|-----|----|----------|
| 22 | Draft a **1-page POC plan** (success metrics, champion, target repo, timeline). | POC plan. |
| 23 | Build a **mini ROI model** (time saved × eng cost; review coverage; throughput). | ROI sheet. |
| 24 | Pick a **vertical** (e.g., the company's space) and tailor the demo + discovery to it. | Tailored demo notes. |
| 25 | **Custom Droid / plugin** (Level 400 stretch): define a specialized droid for a recurring task. | Custom droid config. |
| 26 | Dry-run the **toughest objections**: security veto, model lock-in, "we have Copilot." | Crisp answers. |
| 27 | Re-record the demo (v3). Compare to v1 — you'll see the growth. | Demo recording v3. |
| 28 | **Mock interview**: SE panel style — "walk me through how you'd onboard us." | Mock notes. |
| 29 | Tighten artifacts into a tidy folder you can screen-share. | Portfolio. |
| 30 | Rest + skim docs changelog for anything new. Confirm pricing/features are current. | Confidence. |

## Interview-day proof kit (what to bring)
- The **AGENTS.md** you wrote + a before/after quality example.
- A **Mission** writeup and a **`droid exec` CI** run (screenshot/repo link).
- A **20-min demo** you can give live on your sandbox repo.
- A **discovery question set**, **POC plan**, and **ROI sheet**.
- The **4 competitor one-liners** and **6 objection answers** — cold.

## The meta-tip
SEs are hired for *judgment and communication*, not trivia. Every "teach-back" day matters
more than it looks: being able to **explain it simply and demo it smoothly** is the job. If
you only do three things: write a real AGENTS.md, build the `droid exec` CI step, and rehearse
the demo arc out loud five times.

Sources: [Quickstart](https://docs.factory.ai/cli/getting-started/quickstart) ·
[Power user tactics](https://docs.factory.ai/cli/user-guides/power-user-tactics) ·
[Setup checklist](https://docs.factory.ai/cli/power-user/setup-checklist)
