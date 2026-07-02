# Mock-Interview Drill Bank

> Same method as the Baseten quiz bank: answer **out loud, without notes**, then check
> yourself against the notes. Score each answer 0–2 (0 = blanked, 1 = got there messily,
> 2 = crisp). Re-drill anything under 2. Answers reference the note that covers them.

## Round 1 — Product fluency (Level 100–200)

1. What is Factory in one sentence, and what's the core mental model (vs. autocomplete)? *(01)*
2. Name the four surfaces and one scenario each is built for. *(01)*
3. Walk through the autonomy levels. Which one does `git push` first appear in? *(02)*
4. What does Shift+Tab do? Ctrl+L? Ctrl+N? What's the `!` prefix for? *(02)*
5. What's in a good AGENTS.md, and what should you deliberately leave out? *(03)*
6. A customer's Droid keeps writing plausible-but-wrong code. What's your first diagnostic question? *(03 — context failure, not model failure)*
7. What's the difference between `/context` and `/cost`, and when do you show each in a demo? *(02, 03)*

## Round 2 — Workflows (Level 200–300)

8. Spec Mode: what does it produce, where is it saved, and what buyer anxiety does it answer? *(04)*
9. Missions: what's the worker/validator split and when do Missions beat a single pass? *(04)*
10. Write (out loud) a `droid exec` invocation for a CI step that fixes lint and emits JSON. *(02, 04)*
11. Match the tool: (a) "is this PR safe?" (b) "migrate 200 call sites" (c) "verify the signup flow actually works in a browser" (d) "format staged files pre-commit". *(04 cheat-sheet)*
12. Why would you use `--spec-model` with a different model than execution? What's the cost story? *(04, 05)*
13. What is `-w/--worktree` for and when would you reach for it? *(02)*

## Round 3 — Enterprise & the SE motion (Level 300)

14. A CISO asks "what leaves our network and who controls the model?" — answer using BYOK, Router, and data-flow features. *(05)*
15. Explain hierarchical settings and why "extension-only" matters to a platform team. *(05)*
16. What is Agent Readiness, and how do you use it as a *discovery* tool rather than a dashboard? *(05)*
17. Design a 2-week POC: pick the metric, the repo criteria, and the exit condition. *(05)*
18. The champion loves it but engineering says "we tried an AI tool last year and it wrote garbage." What's your move? *(03 + 05 — grounding demo, before/after AGENTS.md)*
19. Give the ROI framing in under 60 seconds without saying "it depends." *(05)*

## Round 4 — Competitive (rapid fire — 30 seconds each)

20. "...vs Cursor?" *(06)*
21. "...vs Claude Code?" *(06)*
22. "...vs Copilot?" (bonus: why coexistence beats rip-and-replace) *(06)*
23. "...vs Devin?" *(06)*
24. Name one genuine strength of each competitor — conceding credibly. *(06)*
25. An engineer starts a benchmark slugfest. Pull the conversation up a level. *(06 — category, not checklist)*

## Round 5 — Roleplay scenarios (do these with a friend or an AI)

26. **The skeptical staff engineer.** They interrupt your demo at step 2: "I could do that fix faster myself." Redirect to delegation-at-scale without being defensive.
27. **The security veto.** Mid-POC, security freezes agent access. Negotiate a read-only + Spec-Mode-only scope that keeps the POC alive.
28. **The wrong first task.** Champion wants to demo Droid on their gnarliest legacy module first. Talk them into a better wedge task and explain why (readiness, trust curve).
29. **The pricing ambush.** "So what's this cost for 200 engineers?" You don't have exact numbers. Handle it without making one up. *(06 — directional + follow-up)*
30. **Your background.** "You come from inference infra (Baseten prep!) — why does that make you a better Factory SE?" Connect BYOK/self-hosted models and POC-with-metrics muscle. *(08)*

## Scoring

| Total | Read |
|-------|------|
| 50–60 | Interview-ready. Do one live demo rehearsal and stop cramming. |
| 35–49 | Solid base. Re-drill your zeros; they cluster in one note — reread just that one. |
| < 35 | You're reading, not reps-ing. Go do Week-1/2 of the trial plan *(07)*, then come back. |
