# Security policy (CollectiveCortex)

## Non-negotiables
- **Never commit secrets**: API keys, tokens, passwords, private URLs, or personal data.
- If a workflow needs a secret, reference it as: "stored in local `.env`".
- Prefer **sanitized** exports for sharing.

## Redaction rules (quick)
- Redact any `*_API_KEY`, `botToken`, `api_hash`, OAuth tokens, Twilio auth tokens, etc.
- Redact emails/phone numbers unless explicitly intended for public sharing.

## Trust model
- Telegram is transport/coordination only.
- Git is canon; all canon content must be safe to store long-term.
