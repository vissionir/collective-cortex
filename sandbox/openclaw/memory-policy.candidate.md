# Memory policy (OpenClaw) — candidate

STATUS: candidate

## CLAIM
Semantic memory should store only reusable operational mechanisms (protocols/checklists/algorithms), not narratives or ideology.

## HOW_TO_APPLY
- Set memory backend (e.g., LanceDB) with `autoCapture=false`.
- Use manual `memory_store` only when a rule/protocol meets the bar.
- Keep a capture policy file + a state file to rate-limit and dedupe.

## RISKS/LIMITS
- Over-capturing pollutes retrieval; under-capturing loses continuity.
- Always redact secrets; never store credentials in semantic memory.
