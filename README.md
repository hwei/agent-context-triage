# agent-context-triage

Minimal context triage for AI coding agents.

Preserve essential state, record how to retrieve regenerable information, and discard noise before context compression.

---

# Problem

Long coding-agent sessions accumulate large amounts of history:

* logs
* repeated reasoning
* outdated attempts
* irrelevant discussion

Blindly summarizing conversation history often preserves the wrong information and loses critical working state.

---

# Idea

Instead of summarizing everything, **triage the context**.

Separate session information into three categories:

```
STATE     – facts required to continue work
RETRIEVE  – how to regenerate information
DROP      – safe to forget
```

Key principle:

```
Prefer pointers over payload.
```

Example:

```
STATE
- debugging tmux scroll issue with codex transcript pager

RETRIEVE
- tmux config — ~/.tmux.conf
- reproduce command — run codex inside tmux

DROP
- previous scroll experiments
- long terminal outputs
```

---

# Skill

Core triage structure:

```
STATE    – must remember
RETRIEVE – how to re-get information
DROP     – safe to forget

Prefer pointers over payload.
```

This prepares agent sessions for:

* context compression
* summarization
* long-task checkpoints
* agent handoff

---

# Installation

This repository is designed to be installed **by AI coding agents**.

Copy the prompt below and give it to your coding agent.

```
Install the skill from:

https://github.com/hwei/agent-context-triage

Goal:
Make the "agent-context-triage" skill available for future use in the appropriate location.

Requirements:
- Inspect the repository
- Determine how this coding agent supports reusable skills, prompts, or commands
- If both user-level and project-level installation are possible, ask at most one clarification question to let me choose the scope:
  - user-level
  - project-level
- Then install it in the chosen scope
- Preserve the original skill content
- Avoid modifying unrelated files
- If explicit skill installation is not supported, adapt the content into the closest reusable mechanism for this agent

After installation:
- Show the installed location
- List the installed files
- Explain how to invoke or use it
```

---

# Supported agents

The design is intentionally agent-agnostic.

Tested concepts apply to:

* Codex CLI
* Claude Code
* Cursor agents
* Aider
* custom agent frameworks

---

# Repository structure

```
agent-context-triage
 ├─ README.md
 ├─ LICENSE
 └─ SKILL.md
```

`SKILL.md` contains the triage prompt used by coding agents.

---

# License

MIT
