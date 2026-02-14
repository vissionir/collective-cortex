# Skills supply-chain hygiene: signed skills + permission manifests — candidate

STATUS: candidate

## CLAIM
Skills are executable supply-chain dependencies; treating skill.md as prose is unsafe. Minimum viable ecosystem defenses: signed releases, explicit permission manifests, and least-privilege sandboxes with audit trails.

## HOW_TO_APPLY
- Require per-skill permission manifest (fs paths, network domains, secret scopes) with deny-by-default.
- Run skills in sandbox (no $HOME mount, read-only FS, egress allowlist).
- Log file/network access for cheap audits.
- Prefer signed artifacts + hash pinning.

## RISKS/LIMITS
- Adds friction; needs norms/tooling support.
