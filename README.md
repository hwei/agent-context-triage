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

Instead of "summarize everything", triage first. You will preserve operational state and discard noise.

Typical use cases:

- context compression
- long-task checkpoints
- agent handoff
- end-of-day progress snapshots

---

## How to use

This skill is meant to be used immediately before context compression.

Invocation syntax depends on the host agent. Some agents expose installed skills as slash commands, while others require mentioning the skill name directly.

### Codex

After installation, invoke the skill by naming it explicitly in your request, for example:

```text
$agent-context-triage
```

or:

```text
Use agent-context-triage to triage the current session before compacting.
```

If your Codex environment supports a separate compaction command, run that immediately after triage.

### Claude Code

If your Claude Code environment exposes installed skills as slash commands, use:

```text
/agent-context-triage
/compact
```

### General pattern

1. Run the triage skill.
2. Review the triage output in `STATE / RETRIEVE / DROP` format.
3. Immediately compress or checkpoint context.

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
- In `RETRIEVE`, store commands, paths, and URLs rather than full payloads.
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
Make the "agent-context-triage" skill available for future use in this coding agent's native reusable-skill mechanism.

Requirements:
- Inspect the repository and preserve the original skill content.
- Determine this agent's native mechanism for reusable skills, prompts, or commands.
- Prefer native skill installation over adaptation when supported.
- If both user-level and project-level native installation are supported, ask at most one clarification question.
- If only one native scope is supported, install directly in that scope without asking.
- Avoid modifying unrelated files.
- If native skill installation is not supported, adapt the content into the closest reusable mechanism for this agent.

After installation:
- Show the installed location.
- List installed files.
- Explain the exact invocation syntax for this agent.
- If a restart or reload is required for discovery, say so explicitly.
```

---

## Supported agents

The method is agent-agnostic and works anywhere reusable prompts or skills exist.

Common targets:

- Codex
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

- `SKILL.md`: canonical triage prompt
- `README.md`: explanation, installation prompt, and usage guidance

---

## License

MIT
