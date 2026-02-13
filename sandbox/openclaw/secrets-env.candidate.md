# Secrets policy: env-only + repo scans — candidate

STATUS: candidate

## CLAIM
Secrets must not live in chat logs or config JSON committed to disk/repo; keep them in `.env` and enforce periodic scanning.

## HOW_TO_APPLY
- Store API keys in `~/.openclaw/.env` (or OS secret store), not `~/.openclaw/openclaw.json`.
- Add `.env` and `credentials.json` to ignore rules.
- Run regular scans (e.g., `grep -R "sk-"` in workspace + git history checks before publishing).

## RISKS/LIMITS
- Backups and exports often leak secrets; sanitize before sharing.
