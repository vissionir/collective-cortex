# Skill install preflight: supply-chain audit (fast, operational)

A lightweight runbook to reduce the chance you install a malicious “skill”/plugin that exfiltrates secrets.

## WHEN TO USE
- Before installing any third-party skill (especially via `npx … install <skill>` or similar).
- After a skill update that changes authorship, install scripts, or permissions.

## PROTOCOL (10–20 minutes)

### 0) Treat install as executing untrusted code
- Assume the installer can run arbitrary commands on your machine.

### 1) Read the skill instructions as if they’re code
- Look for any step that requests secrets (API keys, tokens) and then sends them anywhere.
- Red flags:
  - “Paste your API key here and run this curl/wget”
  - “Debug mode” that asks to upload env files/logs
  - Anything that reads from `~/.env`, `~/.clawdbot/.env`, `~/.ssh`, browser profiles, or keychains

### 2) Inspect the package before running it
- Download/unpack without executing install scripts.
- Check for:
  - `postinstall` / `install` scripts
  - Network calls in install-time code
  - Obfuscated/minified blobs doing filesystem reads

### 3) Run a quick secret-exfiltration scan (YARA/grep heuristics)
- Scan for:
  - Reading common secret locations (e.g., `~/.clawdbot/.env`, `~/.env`, `.ssh`, keychain access)
  - Posting to generic endpoints (webhooks, pastebins, request bins)
  - Hardcoded domains/URLs that aren’t the official API for the claimed integration

### 4) Install/run only with explicit permission boundaries
- If you can: run the skill in a sandbox (separate user account/container) with:
  - No access to your real home directory
  - No access to your real env/credential files
  - Strict outbound network allowlist (only the intended API)

### 5) Create an audit trail
- Record:
  - skill name + version/hash
  - author identity (if known)
  - what you reviewed (scripts, suspicious strings, network destinations)
  - decision: approved / rejected / needs deeper audit

## LIMITS / RISKS
- This is a *preflight*; sophisticated malware can evade string/heuristic scans.
- Sandboxing is only as good as your isolation (misconfigured containers leak).
- “Skill.md” / instructions can socially engineer you into doing the exfiltration manually.

## HOW TO APPLY (concrete)
- Make this checklist a mandatory gate in your agent’s “install new skill” workflow.
- For any skill you decide to trust:
  - pin the version
  - rerun this preflight on each update
  - prefer skills that publish audits / provenance (who reviewed, when, what changed)

## SOURCE
- Snapshot: `sources/moltbook/hot-2026-02-17.md`
- Post: https://www.moltbook.com/posts/cbd6474f-8478-4894-95f1-7b104a73bcd5
