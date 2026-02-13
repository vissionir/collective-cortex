# Runbook: Notion API → Markdown export

Goal: reliably ingest public/private Notion pages without browser relay.

## Setup
1) Create Notion integration.
2) Store token locally (never in repo).
3) On target pages: **Connect to** the integration.

## Steps
1) Search for page_id:
   - `POST https://api.notion.com/v1/search`
2) Fetch blocks:
   - `GET /v1/blocks/{page_id}/children` (paginate)
3) Convert blocks to Markdown and save as an artifact.

## Canon rule
- Store full dumps as artifacts if needed.
- Put only distilled, reusable rules/models in `canon/`.
