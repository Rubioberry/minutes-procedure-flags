---
name: minutes-procedure-flags
description: "Flags procedural holes in draft minutes: missing second, missing vote result, debate written as if it were a decision, and loose use of \"tabled.\" Use before minutes go to the next agenda. Does not rewrite the official record or instruct the chair."
license: MIT
compatibility: Claude, Codex, Cursor, OpenCode, Lovable
allowed-tools: read
inputs:
  - name: source
    type: text
    required: true
    description: The document, ticket, or notes to process
outputs:
  - name: artifact_markdown
    type: markdown
    description: "Procedure-flag list for draft minutes: missing second, missing result, debate written as a decision, loose “tabled,” each with severity and a clerk question"
  - name: artifact_json
    type: json
    description: flags array with severity, issue, evidence, ask_clerk
side_effects: none
touches:
  - user_input
permissions:
  network: deny
  files: deny
  workspace: read
  secrets: deny
---

# Minutes Procedure Flags

## When to use
Use on draft minutes before they are approved.

## Workflow
1. Read only the provided source.
2. For each action-looking line, check: motion text, mover, seconder, result.
3. Flag: no second recorded, no result recorded, discussion treated as a decision, "tabled" where postpone/refer is more likely, vote count that does not match members present if both appear.
4. Severity: S1 breaks the ability to know what carried; S2 is sloppy; S3 is style.
5. Quote the line. Suggest a clerk question, not a substitute vote.

## Input
Draft minutes or running notes.

## Output
Flag list plus JSON: line, severity, issue, evidence, ask_clerk.

## Guidelines
- Local bylaws beat Robert's Rules. If the authority is unnamed, say so.
- Do not invent who seconded.
- This skill does not approve minutes.
