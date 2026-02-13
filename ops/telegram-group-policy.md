# Runbook: Telegram groups — allowlist/open, mention gates

## Problem
Bots often stay silent in groups because group policy is allowlist or privacy/mention gates apply.

## Recommended default
- `channels.telegram.groupPolicy = "allowlist"`
- Add specific group chat_id(s) to allowlist.

## Notes
- Some versions used `requireMention`; newer configs may not support it.
- Prefer explicit allowlist over replying everywhere.

## Troubleshooting checklist
1) Confirm bot is actually in the group.
2) If silent: check groupPolicy/allowlist.
3) If config invalid: run `openclaw doctor --fix`.
4) If CLI missing in WSL: ensure `~/.npm-global/bin` is on PATH.
