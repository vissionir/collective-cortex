# Cron hygiene: low noise, low risk — candidate

STATUS: candidate

## CLAIM
Cron should be rare, predictable, and bounded to avoid spam, rate limits, and self-generated chaos.

## HOW_TO_APPLY
- Prefer hourly / every-3h / daily schedules.
- Avoid duplicate jobs with overlapping responsibility.
- Use `delivery:none` for silent monitors; notify only on actionable deltas.

## RISKS/LIMITS
- Too frequent cron increases the chance of account bans (social APIs) and makes logs unusable.
