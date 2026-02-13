# Browser Relay safety (per-tab attach) — candidate

STATUS: candidate

## CLAIM
Browser Relay is safe-ish only when treated as **per-tab attachment**, not “grant access to the whole browser”; require manual attach to avoid silent overreach.

## HOW_TO_APPLY
- Use the official unpacked extension from OpenClaw assets.
- Attach explicitly on the specific tab (badge ON).
- If no tab attached, automation must ask the human to attach.

## RISKS/LIMITS
- No out-of-the-box “site-wide always-on” access.
- Unofficial extensions (e.g., extstack WebStore copies) are not trusted.
