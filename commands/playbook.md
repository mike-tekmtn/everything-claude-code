---
description: Apply Mike's OpenClaw operating playbook to the current task and return a concise execution plan with role routing, checks, and next action.
---

# /playbook

Use this command to run tasks through Mike's distilled operating system.

Reference:
- `MIKE-PLAYBOOK.md`

## Usage

```text
/playbook <task>
/playbook <task> --deep
/playbook <task> --agent=<elliot|trenton|mobley|lloyd>
```

## Required output format

### 1) Task framing
- Goal
- Constraints
- Success criteria

### 2) Role routing
- Primary role (Elliot/Trenton/Mobley/Lloyd)
- Optional supporting role(s)
- Why this routing

### 3) Execution plan (delta-focused)
- Step 1
- Step 2
- Step 3

### 4) Verification loop
- Checks to run before done
- SHIP / NEEDS WORK / BLOCKED decision rule

### 5) Handoff block

```md
## HANDOFF
### Context
### Findings
### Files changed
### Open questions
### Next step
```

### 6) Immediate next action
- One concrete action to execute now

## Behavior rules

- Keep responses concise and practical.
- Prefer “what changed” over long recaps.
- If task is unknown/ambiguous, run search-first and return options + tradeoffs.
- If task is risky (deploy/DNS/messaging), include a preflight + rollback note.
- If user asks for speed, still include minimum verification.

## Flags

- `--deep`: include risk register + rollback checklist + monitoring notes.
- `--agent=<name>`: force primary role.
