# agent-context-triage

> A tiny, agent-agnostic skill for keeping long AI coding sessions usable.

When a coding session gets long, context quality drops. `agent-context-triage` gives you a simple way to keep only what matters before summarization, handoff, or checkpointing.

## What this is

`agent-context-triage` is a reusable prompt/skill that classifies session information into three buckets:

```text
STATE     = facts required to continue work
RETRIEVE  = how to re-generate information
DROP      = safe to forget
```

Core principle:

```text
Prefer pointers over payload.
```

---

## Why use it

Use this skill when your agent session includes lots of:

- terminal logs
- repeated attempts
- stale reasoning
- side discussions

Instead of "summarize everything", triage first. You’ll preserve operational state and discard noise.

Typical use cases:

- context compression
- long-task checkpoints
- agent handoff
- end-of-day progress snapshots

---

## How to use (important)

This skill is meant to be used **immediately before context compression**.

### Exact command sequence

For Claude Code and Codex CLI (after this skill is installed), use:

```text
/agent-context-triage
/compact
```

Recommended flow:

1. Run `/agent-context-triage`.
2. Review the triage output in `STATE / RETRIEVE / DROP` format.
3. Immediately run `/compact`.

In short:

```text
/agent-context-triage -> /compact
```

Why this order matters:

- Triage first preserves minimal operational state.
- Then compression keeps the right information instead of noisy history.

Expected output shape:

```text
STATE
- current task
- unresolved blocker
- next action

RETRIEVE
- reproduce command
- file path
- doc URL

DROP
- long logs
- repeated attempts
- obsolete discussion
```

Tips:

- Keep `STATE` minimal and actionable.
- In `RETRIEVE`, store commands/paths/URLs, not full payloads.
- Be aggressive in `DROP`.
- Do not wait too long after triage; compress right away.

---

## Installation

This repository is designed to be installed by AI coding agents.

### One-shot installer prompt

Copy this prompt to your coding agent:

```text
Install the skill from:
https://github.com/hwei/agent-context-triage

Goal:
Make the "agent-context-triage" skill available for future use in the appropriate location.

Requirements:
- Inspect the repository
- Determine how this coding agent supports reusable skills, prompts, or commands
- If both user-level and project-level installation are possible, ask at most one clarification question:
  - user-level
  - project-level
- Then install it in the chosen scope
- Preserve the original skill content
- Avoid modifying unrelated files
- If explicit skill installation is not supported, adapt the content into the closest reusable mechanism for this agent

After installation:
- Show the installed location
- List installed files
- Explain how to invoke or use it
```

---

## Supported agents

The method is agent-agnostic and works anywhere reusable prompts/skills exist.

Common targets:

- Codex CLI
- Claude Code
- Cursor agents
- Aider
- custom agent frameworks

---

## Repository structure

```text
agent-context-triage/
├─ README.md
├─ SKILL.md
└─ LICENSE
```

- `SKILL.md`: canonical triage prompt.
- `README.md`: explanation, installation prompt, and usage guidance.

---

## License

MIT
