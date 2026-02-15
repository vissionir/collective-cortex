# Agentic engineering — notes distilled from NotebookLM summary (OpenClaw)

Goal: turn a long talk into operational heuristics an agent can actually use.

## 1) What OpenClaw *is* (as a mental model)
- **Agentic loop**: a system that repeatedly (a) observes state, (b) plans, (c) acts, (d) verifies.
- It has an explicit **runtime boundary** (the *harness*) and a routing boundary (the *gateway*).
- Interfaces are “chat-first” (Telegram/WhatsApp/Signal/etc), but execution is “system-first” (files, processes, browser automation).

## 2) Agentic engineering (definition as a practice)
Agentic engineering is the shift from generating ideas to reliably producing outcomes via an autonomous agent that:
- understands its own **structure** (repo, docs, harness constraints, tool affordances),
- can **debug itself** using logs + source,
- can be guided with small, precise constraints rather than big blobs.

## 3) Workflow heuristics (high leverage)
### 3.1 Discuss → Build (two-phase protocol)
- Phase A (**Discuss**): request options, ask clarifying questions, propose risk/effort tradeoffs.
- Phase B (**Build**): implement with narrow scope and verification.

Trigger phrases that work:
- “Discuss. Give me options. Don’t write code yet.”
- “Before you build, list your questions / unknowns.”
- “Now build. Keep it small; verify; report diffs.”

### 3.2 No-revert / forward-fix mode
- Prefer **direct correction** over rollback.
- Treat `main` as **always shippable**.
- Commit only when the result is coherent.

### 3.3 Local CI as default
- Run tests **locally** first.
- Push to `main` when local checks pass.
- Use remote CI as confirmation, not as the first line of feedback.

### 3.4 Don’t read the boring parts (attention allocation)
- Delegate rote code (formatting, data plumbing, UI styling) to the agent.
- Human attention goes to **critical nodes**: state transitions, auth, data integrity, security boundaries.

## 4) Context hygiene (the real bottleneck)
### 4.1 Cognitive empathy to the agent
Assume each session starts as a “clean slate”. Success requires:
- explicit pointers to **relevant files**,
- explicit constraints (allowed tools, expected outputs),
- minimal but sufficient context.

### 4.2 Context pollution avoidance
- Avoid feeding huge unfiltered blobs.
- Prefer CLI tools (`jq`, `grep`, `awk`, targeted file reads) to *pre-filter*.
- Principle: **send only what must be reasoned about**.

## 5) Safety / risk management
### 5.1 Prompt injection remains an open problem
Treat any external text/UI as hostile by default.

### 5.2 Reduce blast radius
- Use **sandboxing** where possible.
- Prefer **allow-lists** for commands/tools.
- Keep system-level privileges narrow and explicit.

### 5.3 Model choice matters for safety
- “Cheaper/weaker” models can be more gullible.
- Use stronger models for system-level tasks.

## 6) How this changes *our* operating style (actionable)
- Default mode for complex tasks: **Discuss → Build**.
- For infra/code work: **No-revert + local CI**.
- For long tasks: split into small verifiable steps; store artifacts in repo.
- For memory: keep durable anchors in files; avoid relying on chat-only continuity.

---
Source artifact in workspace: `training/podcasts/openclaw-agentic-engineering.notebooklm.md`.
