# MIKE-PLAYBOOK.md

Distilled from `everything-claude-code` for your OpenClaw workflow (Telegram agents + cron + AWS + web projects).

## Top 10 patterns to use immediately

1. **Context-budget first**
   - Keep replies delta-focused; avoid repeating full plans.
   - Use compact handoff blocks between tasks/threads.
   - Trigger fresh thread at milestone boundaries.

2. **Model routing by task class**
   - Heavy reasoning: primary model.
   - Exploration/listing/triage: lighter sub-agent model.
   - Expensive model only when architecture/debug complexity warrants it.

3. **Structured orchestration handoffs**
   - Always pass: Context, Findings, Files changed, Open questions, Next step.
   - Prevents drift when swapping between Elliot/Lloyd/Mobley/Trenton.

4. **One-agent-one-role discipline**
   - Elliot: strategy/synthesis
   - Trenton: technical risk/security/precision
   - Mobley: implementation/execution
   - Lloyd: polish/comms/presentation

5. **Verification loop before “done”**
   - Build/check -> smoke test -> edge-case pass -> report.
   - Use explicit SHIP / NEEDS WORK / BLOCKED status.

6. **Command-style reusable briefs**
   - Reuse prompt templates for recurring asks (SEO pass, cron design, landing page batch, AWS deploy).
   - Improves consistency and reduces session bloat.

7. **Search-first for unknowns**
   - Gather source evidence before implementation decisions (APIs, infra constraints, indexing behavior).
   - Return with options + tradeoffs, not just one path.

8. **Hooks/checklists for non-skippable ops**
   - For sensitive flows (deploy, DNS, messaging), use preflight checklist:
     - prerequisites
     - dry-run/validation
     - rollback notes
     - post-change verification

9. **Canonical + indexing hygiene bundle**
   - For site launches: canonical, sitemap, robots, host redirect strategy, GSC/Bing verification.
   - Treat this as one atomic SEO baseline task.

10. **Operational snapshots for long work**
   - At major phases output a short control-plane snapshot:
     - active jobs/sessions
     - URLs/env touched
     - pending approvals
     - blockers/next action

---

## Copy/paste templates

### 1) Sub-agent brief template

```md
Goal:
Constraints:
Deliverables:
- D1
- D2
Verification required:
Return format:
- Summary
- Files changed
- Commands run
- Next step
```

### 2) Cron prompt template (quality-safe)

```md
Task:
Scope:
Ranking/prioritization rules:
Output:
1) concise summary
2) ranked list with reasons
3) actionable next step
Guardrails:
- dedupe
- flag uncertainty
- avoid non-local/noise sources
```

### 3) Deployment checklist template

```md
Preflight: auth, target env, backups/snapshots
Apply: infra/content change
Verify: DNS/HTTP/status/log checks
Invalidate/cache refresh
Postflight: user-facing URL checks + note
Rollback plan:
```

---

## What to ignore (for now)

- Multi-harness parity internals not relevant to OpenClaw daily ops.
- Large plugin packaging/install architecture unless you plan to publish your own plugin.
- Language-specific reviewer agents you don’t actively use this month.

---

## Next 3 upgrades I recommend

1. Create a local `prompts/` folder in workspace for your recurring brief templates.
2. Add a tiny “done-report” schema for all sub-agent outputs.
3. Add a weekly cron that audits stale jobs/sessions and reports cleanup candidates.
