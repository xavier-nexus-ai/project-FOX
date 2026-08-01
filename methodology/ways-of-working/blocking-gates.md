# Blocking Gates Reference

Blocking gates are binary pass/fail prerequisites that prevent premature advancement between phases. They are not bureaucracy — they are the mechanism that stops Njin building on weak foundations.

---

## The Core Rule

**If a gate has not passed, the next phase does not start. No exceptions.**

Skipping a gate to hit a deadline creates problems that take twice as long to fix later. The gates exist because they've been broken before.

---

## Gate Types by Framework

### Njin Method (TORQUE)

| Gate | Between Phases | Required Conditions |
|------|----------------|---------------------|
| **Tone of Voice Gate** | Activation > Immersion | ToV guide created AND approved by client |
| **Data Access Gate** | Activation > Immersion | CRM admin access, historical data received, team interviews scheduled, Core 12 logged |
| **Baseline Validated** | Immersion > Methodology Creation | Core 12 validated with client, "before" snapshot confirmed |
| **Stakeholder Approval** | Methodology Creation > Presentation | Internal review passed, draft reviewed by PM and SME |
| **Client Sign-off Gate** | Presentation > CRM Implementation | Client has formally approved the playbook (no outstanding revisions) |
| **Go-Live Gate** | Implementation > Live Monitoring | Pre-launch checklist 100% complete, all automations tested end-to-end, team trained and certified |

### AI Orchestration (90-day build)

| Gate | Between Phases | Required Conditions |
|------|----------------|---------------------|
| **Immersion Complete** | Immersion > Mapping | AI literacy confirmed, AI Possibilities Map done, Industry Report done, stack configured and validated, client can operate agents independently, quick win built |
| **IP Extraction Complete** | Mid-Mapping checkpoint | Business workflows mapped, 2+ frameworks extracted, 3+ SOPs extracted, 5+ judgement calls extracted, methodology named |
| **Mapping Complete** | Mapping > Transformation | All IP extraction gates PLUS methodology structured with phases, diagnostics designed, constraint map created, leverage plan completed |
| **Components Built** | Mid-Transformation checkpoint | All agents built, all skills built, COS schema designed, templates/workflows/tasks/checklists created, CLAUDE.md written, deploy script created |
| **QA Passed** | Pre-deployment | Framework assembled, QA validation passed (all critical checks green), deploy script tested, client trained |

### VIBE OS (Software Development)

| Gate | Between Phases | Required Conditions |
|------|----------------|---------------------|
| **Requirements Defined** | Discovery > Architecture | PRD complete and approved, user stories defined |
| **Architecture Approved** | Architecture > Planning | System design documented, tech stack confirmed, data model approved |
| **Stories Ready** | Planning > Development | All epics broken into stories, acceptance criteria defined, estimates attached |
| **QA Passed** | Development > Deployment | Code reviewed, tests passing, security scan clean, requirements traced |

### AetherFlow (Digital Agency)

| Gate | Between Phases | Required Conditions |
|------|----------------|---------------------|
| **Strategy Approved** | Strategy > Implementation | ICP defined, content strategy approved, SEO plan in place, brand identity confirmed |
| **Phase Complete** | Each implementation phase | Structure > Styling > Interactions > Logic — each complete before next starts |
| **QA Passed** | Implementation > Launch | Accessibility (WCAG 2.1 AA), performance (Core Web Vitals), cross-browser tested |

---

## Universal Gates (Apply Everywhere)

These gates apply to every Njin engagement regardless of framework:

| Gate | When | Required Conditions |
|------|------|---------------------|
| **Contract Gate** | Before any work begins | Contract signed, payment confirmed or terms agreed |
| **Sales Handover Gate** | Before PM takes over | Complete handover bundle delivered (contract, SOW, transcripts, client docs) |
| **Activation Call Gate** | Before kickoff | Onboarding Activation Call held within 72 hours, all access collected |
| **Kickoff Gate** | Before first sprint | Kickoff call held, quick win delivered, sprint plan approved |
| **Phase Exit Gate** | End of every phase | All required deliverables complete, COS updated, client informed |

---

## How Gate Enforcement Works

### In the COS

Every phase in the COS has a `gates` section:

```yaml
gates:
  immersion_complete:
    passed: false
    required:
      - ai_literacy
      - stack_configured
      - quick_win_built
    checked: ""
```

### In practice

1. **Before advancing a phase**, the Orchestrator checks the gate
2. Each required item is verified — is it actually true?
3. If all items pass, `passed: true` and `checked: <timestamp>`
4. If any item fails, the phase does not advance

### If a gate fails

1. Log the failure in the change log with specifics ("Data Access Gate failed: CRM admin access still outstanding")
2. Create a specific client request via the Communication Agent
3. Set a new deadline
4. Do NOT advance the phase
5. Escalate to James if the blocker persists beyond 5 business days

---

## Gate vs Blocker — The Difference

| Concept | Definition |
|---------|-----------|
| **Blocker** | A problem preventing work from progressing right now. Logged, assigned, deadlined. |
| **Gate** | A formal prerequisite between phases. Has explicit pass/fail criteria. |

A blocker might make a gate fail. But a gate is not the same as a blocker — it's a structural checkpoint that exists even when no blockers are present.

---

## Why Gates Get Skipped (And Why You Shouldn't)

**Common pressures to skip:**
- Client deadline is tight
- Deliverable seems "good enough"
- "The client won't notice"
- "We'll fix it later"

**Why you shouldn't:**
- Gates exist because someone built on a weak foundation before and paid for it
- "Fix it later" compounds — the cost grows every day it's not fixed
- Clients absolutely notice when the output doesn't match what they expected
- Rework from a broken gate is always more expensive than pausing to fix it

**The only acceptable gate override:**
James explicitly approves it in writing, with a documented reason and a follow-up plan. Even then, the gate failure is logged in the COS change log.

---

## Gate Decision Examples

### Example 1: Tone of Voice Gate
**Situation:** Client is slow to approve the ToV guide. Playbook writing is next. Deadline pressure.

**Wrong call:** Start writing the playbook in "generic voice" and adjust later.

**Right call:** Pause. The ToV gate exists because generic voice content has to be rewritten, which takes longer than waiting. Chase the ToV approval. Flag the delay to the client clearly: "We cannot proceed until this is approved — here's why."

### Example 2: Data Access Gate
**Situation:** Client has provided some CRM access but not the historical data. Baseline validation is next.

**Wrong call:** Proceed with Core 12 estimates based on what's visible.

**Right call:** Pause. Historical data is a hard blocker for the Baseline Validated gate. Proceed with caveat is not available here — without real data, the constraint diagnosis is guesswork. Chase the data.

### Example 3: Quick Win Built (AI Orchestration)
**Situation:** Immersion is running long. Week 4 is here. The quick win exercise got skipped.

**Wrong call:** Call Immersion complete and start Mapping anyway.

**Right call:** Schedule the quick win build session. The gate exists because clients enter Mapping more energised and engaged after building something tangible. Skipping it creates shallower IP extraction interviews, which directly impacts the framework quality.

---

**Source:** Project `CLAUDE.md` (gates section), AI Orchestration SOP (Quality Gates and Checkpoints), Njin Method playbook SOP (Prerequisite Validation).
