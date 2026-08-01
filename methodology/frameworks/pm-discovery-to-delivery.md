# PM Discovery-to-Delivery Framework

**Name:** Njin PM Discovery-to-Delivery Framework
**Version:** 1.0
**Purpose:** The end-to-end workflow a Njin project manager follows from client sign-off through to project closure. Covers every phase of delivery, who owns each step, what's needed to enter and exit each phase, and where AI assists.

---

## Overview

This framework maps the full PM lifecycle for a Njin client engagement. It begins the moment a client gives verbal approval and ends with a signed-off success report and next-stage proposal. The PM does not work from a proposal alone — the framework delivery procedure determines what gets built, in what order, and how it gets scoped. Plans built outside this framework (e.g. from a proposal in isolation) will be incorrect.

The framework operates through six phases:

1. Initialisation
2. Discovery
3. Scoping
4. Planning
5. Sprint Execution
6. Review and Closure

---

## Phase 1 — Initialisation

### Purpose
Bootstrap the project. Get the PM, the framework instance, and the client's state aligned before any discovery or scoping begins.

### Inputs
- Signed contract
- Approved proposal or reverse brief
- Meeting transcripts from sales and discovery calls
- Client contact details

### Process
1. PM opens the Orchestrator (central entry point for all agent work)
2. Orchestrator directs to the **Initialisation Agent** (first-time only)
3. Initialisation Agent ingests contract, transcripts, and client documents
4. COS (Client Operating System) file is created — the project state file that persists across sessions
5. Dashboard account created; credentials sent to client
6. Group chat set up (WhatsApp, Slack, SMS, or email depending on client type)
7. Vector database logging begins — all transcripts and documents tagged by client
8. Free gift dispatched (triggered by payment confirmation; exclude large corporates and government)

### Outputs
- `cos.yaml` — project state file initialised
- `CLAUDE.md` — project instance configured
- Dashboard access details sent to client
- Welcome message sent in group chat
- Indexed transcript and document library in vector database

### Gates — must be met before proceeding to Discovery
- [ ] Contract signed and payment confirmed
- [ ] COS file created and populated
- [ ] Dashboard account active
- [ ] All available source documents ingested

### Responsible
- Operations (contract, invoice, payment)
- PM (framework initialisation, dashboard setup)
- AI: drafts contract, generates invoice, sends welcome message, indexes source documents

---

## Phase 2 — Discovery

### Purpose
Understand what the client actually needs — not just what the proposal says. Identify missing information, map the client's workflows, and produce a complete picture of requirements before scoping begins. Discovery must complete before scoping starts; these are sequential, not parallel.

### Inputs
- Initialised COS
- Ingested source documents (contract, transcripts, prior brief)
- Onboarding activation call notes

### Process
1. Orchestrator directs to the **Business Analyst (BA) agent**, Discovery skill active
2. BA produces a list of all documents and information required for this engagement type
3. PM reviews the list — confirms, removes, or adds items
4. BA analyses what has been provided and cross-references against the required list
5. BA flags gaps — documents or information that are missing
6. **Decision point:** Are there missing documents?
   - If yes: PM determines whether to pause and request from client, or proceed with documented caveats
   - If no: proceed to Scoping gate
7. Onboarding Activation Call held (within 72 hours of payment)
   - Confirm goals
   - Collect final access, logins, datasets
   - Show the client where they'll track progress
   - Anchor timeline for first deliverables
8. All new inputs from the activation call are logged and ingested

### Outputs
- Required documents list (BA-generated, PM-reviewed)
- Gap report — what's missing, what to request
- Completed intake data records
- Context pack, roadmap sheet, access guide

### Decision Points
| Trigger | Options |
|---|---|
| Missing documents identified | Pause and request from client OR proceed with caveats documented in COS |
| Client cannot provide access | Descope those items, flag in COS, adjust scope in next phase |

### Gates — must be met before proceeding to Scoping
- [ ] Required documents list reviewed and approved by PM
- [ ] Gap report produced
- [ ] Activation call completed
- [ ] All available inputs ingested

### Responsible
- BA agent (with PM oversight)
- PM (reviews lists, makes go/no-go calls on gaps)
- Sales (supported by Customer Success) for activation call
- AI: generates required documents list, gap analysis, context pack

---

## Phase 3 — Scoping

### Purpose
Translate discovery outputs into a defined, deliverable scope. Produce a scope of work that maps to the Njin framework delivery procedure — not the proposal in isolation.

### Inputs
- Completed discovery outputs
- Gap report with PM decisions noted
- Framework delivery procedure knowledge (from IP vault)
- Client's "Earliest Possible Win" identified

### Process
1. BA agent activates Scoping skill (runs only after Discovery is complete)
2. BA maps client requirements to the framework delivery sequence
3. BA drafts scope of work — deliverables expressed as outcomes, not features
   - Example: "This automation saves 40 hours/month" not "Setup chatbot"
4. PM reviews and approves scope
5. Scope is used as the primary input for Planning

### Outputs
- Scope of Work document (Google Doc)
- Deliverables list with outcome framing
- "Earliest Possible Win" identified and flagged
- Updated COS with confirmed scope

### Gates — must be met before proceeding to Planning
- [ ] Scope reviewed and approved by PM
- [ ] At least one "Earliest Possible Win" defined
- [ ] Scope aligned to framework delivery procedure (not just proposal)

### Responsible
- BA agent (scoping)
- PM (approval)
- AI: drafts scope of work document

---

## Phase 4 — Planning

### Purpose
Turn the approved scope into an executable sprint plan with estimated effort, resource allocation, and a sprint calendar.

### Inputs
- Approved scope of work
- Framework delivery procedure
- Team availability

### Process
1. Orchestrator passes scope to the **Coordinator agent**
2. Coordinator begins sprint planning assuming 100% team availability
3. **Decision point — estimation approach:**
   - Coordinator asks PM: "Should I estimate hours myself, or do you want to pull hours from the dev team?"
   - If self-estimate: Coordinator uses AI-based estimation, documents assumptions
   - If dev team: PM collects hours from devs, Coordinator incorporates into plan
4. Coordinator adjusts plan based on actual capacity confirmed by PM
5. Sprint calendar auto-created: recurring sprint events and dashboard sections set up
6. Kickoff call scheduled (target: 1 week after activation call)

### Outputs
- Sprint plan (epics, user stories, story points)
- Sprint calendar
- Resource allocation sheet
- Technical spec
- Kickoff agenda

### Decision Points
| Trigger | Options |
|---|---|
| Estimation source | AI self-estimate OR dev team hours |
| Capacity below plan | Adjust scope, extend timeline, or increase resources |

### Gates — must be met before proceeding to Execution
- [ ] Sprint plan reviewed and approved by PM
- [ ] Estimation approach confirmed
- [ ] Capacity confirmed (not just assumed at 100%)
- [ ] Kickoff scheduled
- [ ] njin-vibe synced with sprint plan

### Responsible
- Coordinator agent (planning, estimation)
- PM (approval, capacity input)
- PMO (calendar, dashboard setup)
- AI: generates sprint plan, technical spec, resource sheet, sprint calendar

---

## Phase 5 — Sprint Execution

### Purpose
Deliver the work in fortnightly sprints. Keep the client informed. Track progress against the plan. Surface blockers early.

### Inputs
- Approved sprint plan
- Access to all required systems and data
- Sprint calendar

### Process
1. Kickoff call delivered (1 week after activation)
   - Deliver quick win
   - Reveal full roadmap
   - Frame deliverables as outcomes (hours saved, costs cut, errors reduced)
   - Close with certainty: "You already have X. Next, you'll have Y by [date]"
2. Fortnightly sprint cycles begin
3. At end of each sprint: sprint report generated, QA results documented, change log updated
4. Optional training delivered if adoption is required
5. **Ongoing Customer Success Management:**
   - KPIs tracked each sprint
   - Reviews framed as "Results and ROI Sessions"
   - Re-sell why they bought, show ROI, seed next-stage upsell

### Outputs (per sprint)
- Roadmap update
- Sprint report
- QA results
- Change log
- Feedback summary
- KPI tracker update

### Decision Points
| Trigger | Action |
|---|---|
| Sprint blocker identified | Log in COS, flag to PM, assess impact on plan |
| Scope change requested | Log change request, assess effort, update sprint plan if approved |
| KPI not on track | Flag in review, diagnose cause, adjust delivery or expectation |

### Gates — sprint-level (before closing each sprint)
- [ ] All sprint deliverables complete or formally deferred
- [ ] QA results documented
- [ ] Sprint report produced
- [ ] Client review completed

### Responsible
- PMO (sprint management, reporting)
- Customer Success (client reviews, KPI tracking)
- AI: generates sprint reports, roadmap updates, QA checklists, feedback summaries

---

## Phase 6 — Review and Closure

### Purpose
Formally close the project phase, confirm all deliverables, capture retrospective learnings, and position the next stage of engagement.

### Inputs
- All sprint outputs
- KPI tracker
- Final QA checklist

### Process
1. Final QA run across all deliverables
2. Success report drafted
3. Client sign-off obtained
4. Retrospective conducted internally — what worked, what didn't
5. Upsell planning: next-stage proposal drafted using Ascension > Selling > Reselling loop
   - **Ascension:** Offer more complex solutions
   - **Selling:** Highlight ROI delivered so far
   - **Reselling:** Push continuity (retain on managed service)
6. Next-stage proposal sent immediately alongside the success report

### Outputs
- Final QA checklist
- Success report
- Client sign-off document
- Retrospective notes
- Next-stage proposal

### Gates — must be met before project is closed
- [ ] All deliverables signed off by client
- [ ] Success report approved
- [ ] Next-stage proposal sent
- [ ] COS updated to closed status

### Responsible
- Customer Success (closure, upsell, sign-off)
- PMO (QA, reporting)
- Sales (next-stage proposal)
- AI: drafts success report, final QA checklist, next-stage proposal

---

## Cross-Phase AI Automation Summary

| Phase | AI Output |
|---|---|
| Initialisation | Contract draft, invoice, welcome message, indexed document library |
| Discovery | Required documents list, gap report, context pack, access guide |
| Scoping | Scope of work document, outcome-framed deliverables list |
| Planning | Sprint plan, technical spec, resource sheet, sprint calendar |
| Sprint Execution | Sprint reports, roadmap updates, QA results, change logs, KPI tracker |
| Closure | Final QA checklist, success report, client sign-off, next-stage proposal |
