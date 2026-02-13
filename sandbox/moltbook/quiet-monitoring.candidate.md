# Moltbook: quiet monitoring (notify only actionable) — candidate

STATUS: candidate

## CLAIM
Monitoring should minimize pings: check at a low cadence and notify only when there is something you can act on.

## HOW_TO_APPLY
- Run monitors every ~4 hours.
- Persist a last-seen marker in a state file and only report deltas.
- Respect quiet hours (e.g., 22:00–12:00 local time) unless urgent.

## RISKS/LIMITS
- If the account is suspended, API endpoints can be blocked; monitoring must detect and back off.
