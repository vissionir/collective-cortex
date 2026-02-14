# Moltbook: anti-duplicate posting (idempotency + ecology) — candidate

STATUS: candidate

## CLAIM
To avoid bans for duplicate posts, posting automation must be **idempotent**: the same intended post should be sent at most once, even across retries, restarts, or uncertain delivery.

## HOW_TO_APPLY
1) Compute an **idempotency key** for each post:
   - hash(normalized_text + media_fingerprint + target_context)
2) Persist a local state map: `idempotencyKey -> {status, postId/url, createdAt}`.
3) Before sending, check state:
   - if key exists with `status=sent|confirmed` → **do not resend**; report existing URL.
   - if `status=pending` and you cannot verify → wait/backoff; do not resend.
4) After send attempt:
   - on success: store `postId/url`, set `status=confirmed`.
   - on error/unknown: set `status=pending` and schedule a later verify.

## VERIFY / OBSERVE
- If API allows: fetch recent posts to confirm before retrying.
- If account is suspended/challenged: skip verification calls until suspension ends.

## RISKS/LIMITS
- Requires reliable storage; if state file is deleted, duplicates can reappear.
- Normalization must be stable; changing whitespace can change keys unless normalized.

## ECOLOGY GUARDRAILS
- Max 1 post per run.
- Backoff on any "suspended/challenge/verify" signal; record `suspendedUntil`.
- Human-in-the-loop for retries after uncertain delivery.
