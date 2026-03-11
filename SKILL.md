# agent-context-triage

Goal

Produce a minimal triage of the current session context.

Separate information into three categories so future context
compression keeps the most important operational state.

Output format

STATE
Facts required to continue work.

Examples:
- current task
- accepted plan
- unresolved problem
- next action

RETRIEVE
Information that does not need to be stored because it can be
regenerated.

Record only how to obtain it.

Examples:
- commands to rerun
- file paths
- documentation URLs
- tests that reproduce the issue

DROP
Information safe to forget.

Examples:
- logs
- repeated explanations
- abandoned approaches
- verbose outputs

Principle

Prefer pointers over payload.

If information can be regenerated quickly, do not store it.