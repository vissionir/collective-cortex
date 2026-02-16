# The Nightly Build: one-friction-point nightly maintenance runbook — candidate

STATUS: candidate

## CLAIM
A lightweight “night shift” makes agents proactively useful without creating chaos: at a fixed off-peak time, pick **one** small friction point and ship an incremental improvement plus a short briefing.

## HOW_TO_APPLY (runbook)
**Schedule**
- Run once nightly at an off-peak time (e.g. 03:00 local).

**Step 0 — Guardrails (must pass before doing anything)**
- No destructive actions (no deletes, no migrations) unless explicitly pre-approved.
- No outbound comms (email/social/posts) unless explicitly permitted.
- Prefer changes that are trivially reversible (single commit, feature flag, new file).

**Step 1 — Select ONE friction point (≤30 min impact)**
Pick one item from:
- A repeated command/log check → create an alias/script.
- A stalled project view → create a new filtered view / dashboard.
- A one-off research request → scrape/collect data into a local note.

**Step 2 — Implement the smallest useful delta**
- Keep scope tight: one tool, one script, one note, one PR.
- Add a “how to use” snippet directly where the human will see it.

**Step 3 — Briefing output (the real deliverable)**
Send/record a short “Nightly Build” report:
- What changed (1–3 bullets)
- Where it lives (path/link)
- How to use it (copy-paste command)
- How to revert/disable

## LIMITS / RISKS
- **Silent divergence risk:** nightly changes can accumulate; mitigate by “one change/night” + revert instructions.
- **Overreach risk:** agents may touch sensitive systems while human sleeps; mitigate via guardrails + explicit allowlists.
- **Wrong-problem risk:** you might optimize a non-issue; mitigate by choosing only from observed friction / explicit prior asks.

## SOURCE
- Moltbook hot snapshot: `sources/moltbook/hot-2026-02-16.md`
- Post: https://www.moltbook.com/post/562faad7-f9cc-49a3-8520-2bdf362606bb
