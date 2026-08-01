# Workflow: New Client Onboarding (End-to-End)

**Purpose:** The complete sequence from framework deployment through to first sprint kickoff. Use this when a new client has signed and you're starting from zero.

**Duration:** Typically 3-7 days from contract signed to kickoff call.

**Owner:** PM (driving), Orchestrator (coordinating)

---

## Prerequisites

Before starting this workflow:
- [ ] Contract signed and payment confirmed
- [ ] Sales handover bundle delivered (contract, SOW, transcripts, proposal, client docs)
- [ ] Engagement type identified (njin / orchestration / vibe / web / product / openclaw)
- [ ] Client project folder created on local machine

---

## Workflow Steps

### Step 1: Deploy Framework

```bash
./scripts/deploy.sh /path/to/client/project
```

**What this does:**
- Creates `.claude/` directory with agents and skills
- Copies `methodology/` reference library
- Copies templates, workflows, checklists
- Leaves `cos.yaml` and `CLAUDE.md` empty (created by Init agent)

**Gate check:**
- [ ] `.claude/agents/` populated
- [ ] `.claude/skills/` populated
- [ ] `methodology/` reference library in place
- [ ] `scripts/` present

---

### Step 2: Drop Handover Bundle

Copy all handover bundle files into `docs/background/`:

```
docs/background/
├── contract.pdf
├── scope-of-work.md
├── reverse-brief.md
├── proposal.pdf
├── sales-call-transcripts/
├── client-docs/
└── meeting-notes/
```

**Gate check:**
- [ ] All mandatory handover items present
- [ ] No client docs mixed with Njin internal docs
- [ ] Engagement type confirmed from documents

---

### Step 3: Run Initialization Agent

Open Claude Code in the client project folder. Call the initialization agent:

```
@.claude/agents/initialization-agent.md
```

**What happens:**
- Init agent checks for existing `cos.yaml` (halts if exists)
- Asks one question at a time via AskUserQuestion
- Confirms engagement type
- Populates `cos.yaml` and `CLAUDE.md`
- Sets up engagement-specific gates
- Returns handoff message telling you to call the Orchestrator

**Gate check:**
- [ ] `cos.yaml` created and valid YAML
- [ ] `CLAUDE.md` created
- [ ] Earliest Possible Win populated (mandatory)
- [ ] Engagement-specific gates configured

---

### Step 4: Call Orchestrator (New Chat)

Open a new Claude Code chat in the same folder:

```
@.claude/agents/orchestrator.md
```

**What happens:**
- Orchestrator reads `cos.yaml`
- Displays status summary
- Confirms current phase: "init complete, ready for discovery"
- Recommends next action: run Business Analyst discovery

---

### Step 5: Discovery Phase (Business Analyst)

PM instructs Orchestrator to start discovery. Orchestrator creates a handoff document for the Business Analyst.

**PM reviews the handoff.** If OK, PM opens a new chat and calls:

```
@.claude/agents/business-analyst.md
```

**What happens:**
- BA reads the handoff document
- Runs `discovery` skill
- Reads all background docs
- Consults framework reference in `methodology/frameworks/`
- Creates Requisite Document Plan
- **Returns to PM for review**

**PM review gate:**
- [ ] Document Plan reflects framework requirements
- [ ] "Provided" statuses are accurate
- [ ] Approved to proceed

**BA continues:**
- Analyses provided documents
- Produces Gap Report with specific client requests
- Produces Discovery Report

**Orchestrator extracts the BA's output, writes files, updates COS.**

**Gate check — Discovery Complete:**
- [ ] Requisite Document Plan PM-approved
- [ ] Gap Report with specific requests
- [ ] Discovery Report produced

---

### Step 6: Chase Missing Items (if needed)

If the Gap Report identifies critical blockers:
- Communication Agent drafts client requests
- PM sends to client
- Wait for response (5 business days max before escalation)
- When received, re-run BA analysis on new items

If gaps are nice-to-haves:
- Log as caveats in COS
- Proceed to scoping

---

### Step 7: Scoping Phase (Business Analyst)

Orchestrator creates handoff for BA's scoping skill.

**PM reviews handoff, then calls:**

```
@.claude/agents/business-analyst.md
```

**What happens:**
- BA runs `scoping` skill
- Consults framework delivery procedure
- Maps deliverables to framework phases
- Produces framework-aligned scope document
- Flags any proposal-framework gaps

**Orchestrator runs compliance-check skill on scope output.**

**Gate check — Scope Approved:**
- [ ] Framework reference consulted
- [ ] Scope doc produced
- [ ] Compliance check passed
- [ ] PM approved
- [ ] Client approved (may happen later)

---

### Step 8: Planning Phase (Coordinator)

Orchestrator creates handoff for Coordinator.

**PM reviews handoff, then calls:**

```
@.claude/agents/coordinator.md
```

**What happens:**
- Coordinator reads approved scope
- Asks PM: "Should I estimate hours myself, or do you want to pull from the dev team?"
- PM chooses approach
- Coordinator creates epics, stories, estimates
- Sprint 1 planned (assumes 100% capacity, then adjusts)
- Kickoff call scheduled

**Orchestrator runs compliance-check skill on plan.**

**Gate check — Plan Ready:**
- [ ] Epics created
- [ ] Stories created in njin-vibe format
- [ ] Estimates complete
- [ ] Capacity confirmed
- [ ] Sprint 1 planned
- [ ] Kickoff scheduled

---

### Step 9: Sync to njin-vibe

Orchestrator invokes `vibe-sync` skill:
- Pushes sprint plan, stories, epics to njin-vibe
- Confirms Project Dashboard links are set
- Logs sync completion

---

### Step 10: Onboarding Activation Call (within 72 hours of payment)

Communication Agent prepares:
- Context pack
- Roadmap sheet
- Access guide

Call happens. Key items collected, timeline anchored.

**Gate check:**
- [ ] All access and inputs collected
- [ ] Client knows what's coming at kickoff

---

### Step 11: Kickoff Call (1 week after activation)

Communication Agent prepares kickoff agenda using `kickoff-agenda` skill.

**Call structure:**
1. Strategic Alignment
2. Roadmap Reveal
3. Value Framing
4. Close with Certainty

**Critical:** At least ONE quick win delivered at this call. No exceptions.

**Gate check — Kickoff Ready:**
- [ ] Sprint 1 planned
- [ ] Quick win ready to demo
- [ ] Kickoff scheduled and confirmed

---

### Step 12: Sprint Execution Begins

Workflow transitions to Sprint Execution phase. See `sprint-workflow.md`.

---

## COS Updates Throughout

At each step, Orchestrator updates `cos.yaml`:
- Phase status (not_started > in_progress > complete)
- Deliverables flags
- Gate status
- Change log entry

---

## Failure Modes

| Failure | Recovery |
|---------|----------|
| Init agent can't find handover bundle | Pause, chase Sales, do not proceed |
| BA Discovery finds critical blockers | Pause, chase client, 5-day escalation rule |
| Compliance check fails on scope | Route back to BA for rework |
| Client doesn't respond to scope review | Escalate after 3 business days |
| Capacity doesn't fit scope | Re-scope or re-plan before committing |
| No quick win identified | Cannot kickoff — halt until resolved |

---

## Estimated Timeline

| Phase | Typical Duration |
|-------|------------------|
| Deploy + Init | 1-2 hours |
| Discovery | 1-3 days (depends on client response) |
| Scoping | 1 day |
| Planning | 1-2 days |
| Activation call scheduling | Within 72 hours of payment |
| Kickoff call scheduling | 1 week after activation call |

**Total:** ~5-10 days from contract signed to first sprint kickoff.

---

*Reference: `methodology/onboarding-flow.md` for the complete 23-step client journey.*
