# COS-First Protocol

The Client Operating System (`cos.yaml`) is the single source of truth for every project. This document defines how to read it, update it, and use it to drive every decision.

---

## The Core Rule

**Read COS before every decision. Update COS after every meaningful change. If it's not in the COS, it didn't happen.**

---

## What the COS Tracks

Every project's `cos.yaml` contains:

| Section | Purpose |
|---------|---------|
| `program` or `client` | Basic identity — name, company, industry, engagement type |
| `business_health` | Key metrics — for Njin Method clients, the Core 12 |
| `phase` | Current phase, status, deliverables, gates |
| `ip_vault` (for AI Orchestration) | Extracted IP counts and source materials |
| `framework_build` (for AI Orchestration) | Components planned vs built |
| `gates` | Blocking gates and their pass/fail status |
| `change_log` | Audit trail of every meaningful change |

---

## Reading the COS

At the start of every session:

1. **Open `cos.yaml`** — first action, always
2. **Identify the current phase** — this tells you what work is active
3. **Check the change log** — what happened in the previous session
4. **Check the gates** — is anything blocking advancement?
5. **Check outstanding deliverables** — what's due next?

**Only after reading the COS should you act on anything.**

If you catch yourself asking "what's next?" — you haven't read the COS yet.

---

## Updating the COS

Update the COS when any of these happen:

| Event | Update |
|-------|--------|
| A deliverable is completed | Mark it true/complete in the phase deliverables |
| A phase gate passes | Update gates section, advance phase if warranted |
| A blocker is identified | Log in the relevant section with owner and deadline |
| A judgement call is made | Add to change_log with reasoning |
| A sprint closes | Sprint results, velocity, carry-forward items |
| A client decision is made | Log in change_log with client name and date |
| A framework component is built | Update framework_build counts and list |
| A new source material is added | Add to ip_vault.source_materials |

**Never silently skip an update.** Hidden state creates problems in future sessions.

---

## Change Log Conventions

Every change log entry has:

```yaml
- date: "2026-04-09"
  phase: "immersion"
  agent: "orchestrator"
  change: "Clear, specific description of what changed and why."
```

**Good entries:**
- "Phase A Step A1 complete — all source materials refined and indexed. Step A2 IP vault extraction started."
- "Discovery Gap Report delivered to PM. CRM access still outstanding from client, escalated. Proceeding with caveat on brand guidelines."
- "Sprint 3 closed. Velocity 28h (up from 22h). One story carried forward: email automation integration blocked on Xero API access."

**Bad entries:**
- "Updates"
- "Various changes"
- "Progress"

If you can't write a specific one-sentence change description, you don't have anything worth logging.

---

## COS Hygiene

### Things to avoid
- **Fabricating values.** Empty fields are better than made-up ones. If you don't know the value, leave it blank with `status: "unknown"`.
- **Duplicate state.** Don't track the same thing in two places. If it's in the COS, it's not in memory or CLAUDE.md.
- **Silent defaults.** Every field should either have a real value or explicitly be marked as not-yet-known.
- **Stale timestamps.** Update `last_updated` on every meaningful edit.

### Things to maintain
- **Phase status accuracy.** If a phase is "not_started" in the COS but work is happening, that's a bug. Fix it.
- **Gate status accuracy.** If a gate is "passed: true" but the requirements aren't actually met, that's a lie. Fix it.
- **Source materials list.** Every document fed into the framework gets added to `ip_vault.source_materials` with `processed: true/false`.

---

## COS vs CLAUDE.md vs Memory

Three places where project state can live. Know the difference:

| File | Purpose | When to use |
|------|---------|-------------|
| `cos.yaml` | Structured project state, phase tracking, deliverables, gates | The authoritative state file — always |
| `CLAUDE.md` | Operational guidance for agents, navigation, key principles | Instructions for how to work, not what the current state is |
| `memory/` | Cross-session learnings, user preferences, feedback | Unstructured context that carries between projects |

**Rule:** Don't duplicate COS data in CLAUDE.md or memory. The COS is the truth. Other files point to the COS.

---

## What the COS Is NOT

- **Not a task tracker.** Day-to-day tasks live in Reclaim, Notion, or njin-vibe. The COS tracks milestones and state, not individual todos.
- **Not a log of activity.** The change log captures meaningful changes, not every tool call.
- **Not a notepad.** Observations and musings go in memory, not the COS.
- **Not a roadmap.** Long-term vision goes in CLAUDE.md or project briefs. COS tracks current state.

---

## COS-First Protocol in Multi-Agent Workflows

When the Orchestrator spawns a specialist agent:

1. Orchestrator reads current COS
2. Orchestrator creates a handoff document that includes relevant COS context
3. Specialist agent reads the handoff document (cannot directly write back to COS — sandbox constraint)
4. Specialist agent returns output in its response
5. Orchestrator extracts the output and writes the appropriate COS updates
6. Orchestrator updates the change log with what the specialist did

**The Orchestrator owns the COS.** Specialist agents never write to it directly.

---

**Source:** Global `CLAUDE.md` (COS-First Protocol), project `CLAUDE.md`, AI Orchestration SOP Section 12 (COS Management Protocol).
