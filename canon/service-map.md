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

## TODO: add other connected services
- Telegram userbot? Notion? GitHub? etc.

## Agent rule
If the user asks "how do we do X" and X is listed here, do not ask basic questions first — start from this map and propose the concrete API call / script.
