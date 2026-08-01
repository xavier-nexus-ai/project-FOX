# Client Onboarding Pipeline

**Name:** Njin Client Onboarding Pipeline
**Version:** 1.0
**Purpose:** The structured pipeline that takes a prospective client from initial contact through to active project execution. Defines each of the 23 steps, the phase they belong to, who owns them, what AI automates, and the decision points and human checkpoints required.

---

## Overview

The onboarding pipeline has five phases:

1. **Prospecting** — Sales activity up to verbal approval
2. **Project Initiation** — Contract, invoice, and payment
3. **Project Planning** — Dashboard, intake, and activation call
4. **Project Execution** — Kickoff, sprints, and ongoing delivery
5. **Closure** — Phase completion and next-stage proposal

The pipeline is designed around certainty and speed. The client must feel, at every step, that delivery is already in motion. Every human touchpoint has an AI-assisted output. Every stage transition is triggered either by a client action (e.g. approval, payment) or an internal milestone.

---

## Phase 1 — Prospecting (Steps 1-2)

### Step 1: Initial Sales Call and Interest

| Field | Detail |
|---|---|
| **Client experience** | Books call via sales CRM |
| **Internal process** | Added to GHL pipeline |
| **Responsible** | Sales |
| **AI automations** | Research, lead scoring, meeting transcripts |
| **Location** | GHL |
| **Key note** | Anchor call around an Activation Promise: "Within 7 days of payment, you'll have X running and already saving you Y hours." Certainty beats information. |
| **Human checkpoint** | Sales must identify and anchor the Activation Promise on this call |

### Step 2: Brief or Reverse Brief

| Field | Detail |
|---|---|
| **Client experience** | Discovery conversation |
| **Internal process** | Reverse Brief drafted and sent for client approval |
| **Responsible** | Sales |
| **AI automations** | Reverse Brief drafted as email |
| **Timeline** | No more than 24 business hours after last contact |
| **Location** | GHL |
| **Key note** | Structure: Problem > Cost of Problem |
| **Human checkpoint** | Sales reviews AI draft before sending; client must explicitly approve |

---

## Phase 2 — Project Initiation (Steps 3-8)

### Step 3: Scope of Work

| Field | Detail |
|---|---|
| **Client experience** | Receives reverse brief as confirmation of high-level requirements |
| **Internal process** | Define deliverables and resources |
| **Responsible** | Sales / Product |
| **AI automations** | Draft Scope of Work (Google Doc) |
| **Trigger** | Manual — client approves reverse brief, staff advance pipeline stage |
| **Key note** | Always include "Earliest Possible Win" as a deliverable |
| **Decision point** | Is the reverse brief approved? If not, loop back to Step 2. |

### Step 4: Proposal

| Field | Detail |
|---|---|
| **Client experience** | Receives pricing, timeline, and deliverables |
| **Internal process** | Proposal drafted |
| **Responsible** | Sales |
| **AI automations** | Proposal PDF |
| **Key note** | Translate deliverables into outcomes — "This saves 40 hours/month" not "Setup chatbot" |
| **Human checkpoint** | Sales reviews outcome framing before sending |

### Step 5: Verbal Go-Ahead

| Field | Detail |
|---|---|
| **Client experience** | Gives verbal approval on call |
| **Internal process** | Marked in CRM to trigger contract automation |
| **Responsible** | Sales |
| **AI automations** | CRM approval log |
| **Decision point** | Verbal approval received? If yes, triggers Step 6. If no, proposal follow-up sequence continues. |

### Step 6: Automated Contract Send

| Field | Detail |
|---|---|
| **Internal process** | Contract generated from proposal data, sent for e-signature |
| **Responsible** | Operations |
| **AI automations** | Contract draft, signed contract record |
| **Trigger** | Automatic on CRM verbal approval log |

### Step 7: Automated Invoice Send

| Field | Detail |
|---|---|
| **Internal process** | Invoice sent immediately after contract is signed via Xero integration |
| **Responsible** | Operations |
| **AI automations** | Invoice generation |
| **Trigger** | Automatic on contract signed event |

### Step 8: Payment Nurture and Confirmation

| Field | Detail |
|---|---|
| **Internal process** | Custom reminder sequence + Xero reminders; auto-reconciliation when paid |
| **Responsible** | Operations |
| **AI automations** | Payment confirmation log |
| **Decision point** | Payment confirmed? If yes, triggers Steps 9-12. If no, nurture sequence continues. |

---

## Phase 3 — Project Planning (Steps 9-16)

### Step 9: Free Gift Dispatch

| Field | Detail |
|---|---|
| **Internal process** | Physical gift dispatched; client message: "Whilst you enjoy this, we're already building your first automation" |
| **Responsible** | Operations |
| **AI automations** | Gift order confirmation |
| **Trigger** | Payment confirmation only |
| **Human checkpoint** | Check if client is a large corporate or government — if yes, skip gift |

### Step 10: Dashboard Account Creation

| Field | Detail |
|---|---|
| **Internal process** | Internal njin-vibe dashboard; credentials sent in group chat (or email for phase 1 clients) |
| **Responsible** | PMO |
| **AI automations** | Dashboard access details |
| **Trigger** | Payment confirmation |

### Step 11: Dashboard Onboarding

| Field | Detail |
|---|---|
| **Client experience** | Interactive onboarding flow within the dashboard |
| **Internal process** | Replaces manual questionnaires; collects key project info |
| **Responsible** | PMO |
| **AI automations** | Intake data records |

### Step 12: Group Chat Setup

| Field | Detail |
|---|---|
| **Internal process** | WhatsApp or Slack group created post-payment; welcome message sent |
| **Responsible** | PMO |
| **AI automations** | Welcome message template |
| **Human checkpoint** | Confirm preferred channel — WhatsApp/Slack for SME, consider SMS/email for corporate |

### Step 13: Vector Database Logging

| Field | Detail |
|---|---|
| **Internal process** | All meeting transcripts and documents stored and tagged by client |
| **Responsible** | PMO / Technical |
| **AI automations** | Indexed transcript and document library |

### Step 14: Onboarding Activation Call (within 72 hours)

This is a critical human checkpoint. It is not a discovery call — it is a confidence-building, expectation-setting conversation.

| Field | Detail |
|---|---|
| **Responsible** | Sales (supported by Customer Success) |
| **AI automations** | Context pack, roadmap sheet, access guide |

**Call structure:**
1. Welcome and framing: "This call gets everything aligned so we can deliver your first [deliverable] at kickoff"
2. Confirm goals: re-state the top outcomes the client wants
3. Information gathering: collect all required access, logins, datasets
4. Dashboard overview: show where they'll track progress and log tickets
5. Timeline anchor: reiterate kickoff date and promise of first deliverables
6. Confidence close: "We now have everything we need. Expect your first [deliverable] live at kickoff"

**Human checkpoint:** PM must confirm that all required access and inputs have been collected before the call closes.

### Step 15: Internal Planning

| Field | Detail |
|---|---|
| **Internal process** | Internal team alignment and resource allocation |
| **Responsible** | Customer Success (supported by Sales) |
| **AI automations** | Internal planning documents |

### Step 16: Kickoff Scheduling Automation

| Field | Detail |
|---|---|
| **Internal process** | Triggered after onboarding activation call; kickoff event auto-created |
| **Responsible** | PMO |
| **AI automations** | Kickoff agenda |
| **Trigger** | Automatic after Step 14 completed |

---

## Phase 4 — Project Execution (Steps 17-21)

### Step 17: Kickoff Call (1 week after activation call)

This is the first client-facing delivery moment. At least one quick win must be delivered here.

| Field | Detail |
|---|---|
| **Responsible** | Customer Success (supported by PMO) |
| **AI automations** | Sprint plan, technical spec, resource sheet |

**Call structure:**
1. Strategic alignment: confirm outcomes and priorities
2. Roadmap reveal: show full timeline and milestones
3. Value framing: translate each deliverable into hours saved, costs cut, or errors reduced
4. Close with certainty: "You've already got X. Next, you'll get Y by [date]"

**Human checkpoint:** At least one deliverable must be ready to show or hand over at this call.

### Step 18: Sprint Scheduling Automation

| Field | Detail |
|---|---|
| **Internal process** | Post-kickoff: recurring sprint events and dashboard sections auto-created |
| **Responsible** | PMO |
| **AI automations** | Sprint calendar |
| **Trigger** | Automatic after kickoff call logged |

### Step 19: Optional Training Module

| Field | Detail |
|---|---|
| **Client experience** | Live or recorded workshop delivered if adoption is required |
| **Responsible** | Customer Success |
| **Key note** | Frame as bonus value: "We don't just build — we empower your team to scale with it" |
| **Decision point** | Is training required for this engagement? If yes, schedule within first sprint cycle. |

### Step 20: First Delivery Cycle (Fortnightly Sprints)

| Field | Detail |
|---|---|
| **Client experience** | Reviews deliverables at end of each sprint |
| **Internal process** | Executes sprints per plan |
| **Responsible** | PMO |
| **AI automations** | Roadmap update, sprint report, QA results, change log |

### Step 21: Ongoing Customer Success Management

| Field | Detail |
|---|---|
| **Client experience** | Attends regular reviews |
| **Internal process** | Tracks KPIs against targets |
| **Responsible** | Customer Success |
| **AI automations** | Feedback summary, KPI tracker, updated notes |
| **Key note** | Frame all reviews as "Results and ROI Sessions." Always re-sell why they bought, show ROI, and seed next-stage upsell. |

---

## Phase 5 — Closure (Steps 22-23)

### Step 22: Project Phase Completion

| Field | Detail |
|---|---|
| **Client experience** | Receives final deliverables and success report |
| **Internal process** | Retrospective and upsell planning |
| **Responsible** | Customer Success (supported by PMO) |
| **AI automations** | Final QA checklist, success report, customer sign-off, next-stage proposal |
| **Human checkpoint** | PM and Customer Success must formally confirm all deliverables are complete before issuing success report |

### Step 23: Next-Stage Proposal

| Field | Detail |
|---|---|
| **Client experience** | Receives continuity, upsell, or cross-sell offer alongside the success report |
| **Internal process** | Draft upsell using Ascension > Selling > Reselling loop |
| **Responsible** | Sales (supported by Customer Success) |
| **AI automations** | Proposal template |

**Ascension > Selling > Reselling loop:**
- **Ascension:** Offer more complex or higher-value solutions
- **Selling:** Highlight ROI delivered so far
- **Reselling:** Push continuity — retain client on managed service

---

## Decision Points Summary

| Step | Decision | Outcome |
|---|---|---|
| 2 | Client approves reverse brief? | Yes > Step 3. No > rework reverse brief. |
| 5 | Verbal go-ahead received? | Yes > Step 6. No > follow-up sequence. |
| 8 | Payment confirmed? | Yes > Steps 9-12. No > nurture sequence. |
| 9 | Is client a corporate or government? | Yes > skip gift. No > dispatch gift. |
| 14 | All access and inputs collected? | Yes > close call, proceed. No > document gaps, follow up. |
| 19 | Is training required? | Yes > schedule. No > skip. |

---

## Human Checkpoint Summary

| Step | Who | What They Must Do |
|---|---|---|
| 1 | Sales | Anchor the Activation Promise on the call |
| 2 | Sales | Review AI draft of reverse brief before sending |
| 4 | Sales | Verify outcome framing in proposal before sending |
| 9 | Operations | Check client type before dispatching gift |
| 12 | PMO | Confirm preferred communication channel |
| 14 | PM / Customer Success | Confirm all access and inputs collected |
| 17 | Customer Success | Confirm a quick win is ready to deliver |
| 22 | PM + Customer Success | Formally confirm all deliverables complete |
