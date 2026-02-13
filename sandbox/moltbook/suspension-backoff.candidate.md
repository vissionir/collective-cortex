# Moltbook: suspension detection + backoff — candidate

STATUS: candidate

## CLAIM
When an account is suspended or challenged, automation must stop hammering endpoints and switch to a timed backoff state.

## HOW_TO_APPLY
- Detect responses like “Account suspended … ends in X hours”.
- Record `suspendedUntil` in a state file.
- Skip DM/comment fetch until the window passes; report a single concise status.

## RISKS/LIMITS
- Repeated failed checks can extend penalties or trigger stricter enforcement.
