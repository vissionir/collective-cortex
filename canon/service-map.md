# Service Map (API-connected services) — single source of truth

Purpose: stop "we did this before" amnesia. This file is what the agent reads first when a task mentions any external service/API.

## Moltbook
- Base URL: https://www.moltbook.com/api/v1
- Auth: Bearer token from `~/.config/moltbook/credentials.json` (fields: `api_key` / `apiKey` / `token`).
- Known endpoints used:
  - GET /agents/me
  - GET /agents/dm/check
  - GET /posts?sort=new|hot
  - POST /posts  (rate limit: 1 post / 30 minutes)

## OpenClaw / internal
- Workspace root: /Users/denisalesev/clawd
- Canon repos:
  - collective-cortex (training + protocols)
  - eternals-brain (ETERNALS ops/protocols)
  - quartz (Post-Ego site)

## AgentMail (email)
- Purpose: send/receive task-relevant emails with minimal manual overhead.
- Credentials/state (local):
  - `memory/agentmail-state.json`
  - `memory/agentmail-state.json` is the canonical local state anchor; update it when sent/processed.
- Notes:
  - Prefer “write-ahead logging”: draft → persist → send → persist result.

## Twitter / X
- Purpose: monitoring + posting with rate limiting/backoff.
- State (local):
  - `tmp_twitter/` (artifacts)
  - `memory/` daily logs when important.
- Ops lessons: unified rate limiting + adaptive backoff; reliable send with retries.

## GitHub
### Post-Ego
- Repo: https://github.com/vissionir/Post_ego
- Site: GitHub Pages project site (base includes `/Post_ego/`).
- Local path: `quartz/`
- Default workflow:
  - edit in `quartz/` → `git status` → commit → push.

### collective-cortex
- Repo: https://github.com/vissionir/collective-cortex
- Local path: `collective-cortex/`
- Use for: agent training, protocols, service map, operational memory.

## TODO: verify & fill exact credential locations
- AgentMail provider details (SMTP/IMAP vs API).
- Twitter auth file/env vars.

## Agent rule
If the user asks "how do we do X" and X is listed here, do not ask basic questions first — start from this map and propose the concrete API call / script.
