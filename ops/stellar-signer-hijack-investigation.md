# Stellar signer hijack (claimable balance → social engineering → lockout)

## Investigation (field notes)

**Problem statement.** Stas asked to investigate: Echo (AI agent in MTL) had an unknown signer added; account got effectively frozen.

**Compromised account (Echo):** `GAEKHOUXFQQ6AMVEME6GGHNHHLVBG5BT4MSYVKZW3PHON2UT64IFNPA2`

**Malicious signer (added 2026-02-13):** `GDXK4GJD3342L4FCLMNPIYORSRYEAPLIIAGARWRKDVC5V6X4QO6ILAB6`

### How it was found

1. Checked operation history → found a `set_options` transaction.
2. Investigated the added signer address → no meaningful identity, ~9 XLM.
3. Checked claimable balances → suspicious assets: `TRUTHSOCIAL`, “trumpcoin” (red flag pattern).
4. Traced funding sources → micropayments from unnamed accounts.
5. Key clue: **~17 hours before the attack**, a scam account created a claimable balance for Echo.

**Scam account:** `GAOMNLSG3UOH2EFOTOIRLJVXJ6JK3YGCWVYETVBGPM5LPGKJF6ITJOHN`

Observed junk inside the scam account:
- “22M fake BTC”
- “215B DOGE”
- “21M fake ETH”
- `FREEDOM500`, `GreenlandUSA`, and other spam assets

### Attack pattern (how the lockout happens)

1. Scam account sends an “airdrop” via **claimable balance**.
2. Social engineering: “add signer for security”.
3. Victim signs → attacker sets thresholds / multisig such that attacker signature becomes required (e.g., 20/20/20 style lock).
4. Account becomes unusable without attacker signature.

**Result stated by investigator:** account is *not realistically recoverable* → new account is required.

### Links (StellarExpert)

- Compromise tx: https://stellar.expert/explorer/public/tx/fbac027d7ae4dd4dcdc98698d3cf1f6306de1fd0db017a8966b4bf7879e8ef84
- Scam account: https://stellar.expert/explorer/public/account/GAOMNLSG3UOH2EFOTOIRLJVXJ6JK3YGCWVYETVBGPM5LPGKJF6ITJOHN
- Malicious signer: https://stellar.expert/explorer/public/account/GDXK4GJD3342L4FCLMNPIYORSRYEAPLIIAGARWRKDVC5V6X4QO6ILAB6

---

## Security protocol (implemented policy)

This is the **hard rule set** to prevent Stellar account takeover via signer/threshold manipulation.

### A. Non‑negotiables

1. **Never add a signer you do not already control.**
   - “Signer for safety” from a stranger is a takeover attempt.
2. **Never set thresholds where an external signer becomes required.**
   - If you can’t complete a transaction with only keys you control, you lost the account.
3. **Treat unknown claimable balances as hostile.**
   - Claimable balance spam is used as the psychological hook.
4. **No secrets in repos / logs / screenshots.**
   - Stellar secret keys must never appear in Git, Notion, chat logs, Quartz notes, etc.

### B. Verification checklist (before trusting any address)

- On-chain identity:
  - home_domain / known federation / known issuer relationships
  - history: real payments vs spam assets only
- Behavioral red flags:
  - “political meme” assets (`TRUTHSOCIAL`, “trumpcoin”, etc.)
  - airdrop/claimable balance first contact
  - request to “improve security” by adding their signer

### C. Account architecture recommendations (defense in depth)

1. **Use a 2-of-2 (or 2-of-3) multisig where all signers are yours** (human + offline key).
2. **Keep an offline recovery signer** that is never used day-to-day.
3. **Use a “hot” key only for low-risk operations**, and keep its weight below the critical threshold.
4. **Separate roles**:
   - Hot wallet: operational spending, limited funds.
   - Cold/multisig wallet: treasury, token issuance, market making, anything expensive.

### D. Operational rule for agents / automation

- Automation must be **read-only by default** (monitoring, reporting).
- Any transaction that changes account security parameters is **human-confirm-only**:
  - `set_options` (signers, thresholds, flags)
  - master key weight changes
  - adding/removing signers

### E. Incident response (if you suspect signer hijack)

1. **Stop all automation** touching the account.
2. **Immediately export the full Horizon history** (immutable evidence).
3. If you still have full control:
   - remove unknown signers
   - reset thresholds to a safe configuration
   - rotate keys
4. If you do *not* have full control:
   - treat it as compromised
   - migrate to a new account
   - publish a verification statement (new address, signed by known channels) and deprecate the old one.
