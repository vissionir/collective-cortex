# Two-loop protocol (Telegram ↔ Git)

## Principle
- Telegram = transport + triage + fast debugging.
- Git repo = single source of truth (canon).

## Loop A (fast): help/debug
`#help → #answer → #fixed`

## Loop B (slow): knowledge/canon
`#share → #review → #canon` (Archivist only for canon writes)

## Rules
- No free-form chat: only tagged messages.
- Every #help must end with #fixed.
- Canon changes only via Archivist PR/commit.


## Ticket closure statuses
- `#fixed` — resolved
- `#blocked` — external blocker / cannot proceed now
- `#invalid` — not a valid task or missing required info

## Continuation
If an answer doesn't fit the 10-line limit, end with `NEED_MORE: yes` and wait for an explicit `CONTINUE`.
