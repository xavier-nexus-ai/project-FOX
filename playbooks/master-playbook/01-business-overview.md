# Business Overview

**Playbook:** Fox Group Master Playbook (Cross-Sell and Monetisation)
**Version:** 2.0
**Created:** 2026-03-12
**Owner:** James
**Status:** Active

---

## Purpose

A complete picture of Fox Group. Who the businesses are. What is broken. How the new system fixes it.

---

## Engagement Scope (Important)

This master playbook covers **FFG and FHL only**. UMI Loans is part of the Fox Group ecosystem and shows up in the group context throughout this document, but UMI is not in scope for either playbook (Cross-Selling & Monetisation, or Pre-Sales SDR).

UMI runs its own systems, its own customer base, and its own model. The group still benefits from a UMI graduation pathway (direct UMI clients eventually moving up to FFG or FHL once their credit recovers), but that pathway is out of scope for this build.

When UMI is mentioned in this playbook, treat it as background, not a workstream.

---

## Service Description

Fox Group operates three financial services businesses under one ownership in Queensland.

**Fox Finance Group (FFG)** is an asset finance brokerage. It matches borrowers with lenders for car loans, personal loans, equipment finance, debt consolidation, and commercial lending. FFG earns a commission when a deal settles. It does not hold loans on its books.

**Fox Home Loans (FHL)** is a mortgage brokerage. It helps clients with home loans, investment property lending, refinancing, and commercial property. FHL earns upfront commission, trail commission (0.65% of the loan balance per year), and broker fees.

**UMI Loans (UMI)** is a lender. It provides secured car loans to sub-prime borrowers (people who have been turned down elsewhere). UMI holds its own loan book of approximately $28 million and earns interest income directly.

All three brands share one MD (Nathan Drew), one group vision, and one physical operation on the Sunshine Coast. Until now they have run as three separate businesses with three separate systems and no shared view of their customers. That is the problem the playbooks fix for FFG and FHL. UMI sits alongside, not inside, the build.

### Brand Positions

| Brand | Position | Hero Story |
|-------|----------|------------|
| FFG | Lifestyle Partner | "Helping you say yes to the life you want." |
| FHL | Wealth and Security Partner | "Guiding you toward long-term wealth and family security." |
| UMI | Second Chance Partner | "When life doesn't go to plan, we help you get back on track." |

---

## Current State

### The Silo Problem

Each business runs its own loan management system:
- FFG uses Ambition (has API, CSV export feeds GHL)
- FHL uses Infynity (formerly Infynity; CSV export feeds GHL)
- UMI uses a proprietary system built by the in-house CTO (out of playbook scope)

There is no unified FFG-FHL customer database today. A client who has a car loan with FFG and a mortgage with another lender sits in Ambition only. FHL does not know they exist. If that client could benefit from a FHL refinance, no one surfaces that opportunity unless a broker happens to remember. Brokers are good at remembering. They are not infallible.

Cross-sell between FFG and FHL is manual and inconsistent. The internal target is 20 cross-referrals per month (10 each way). It is underperforming. No system. No tracking. No automation. That is the gap.

Post-settlement nurture is broken. The current FFG sequence is 6 emails on SendGrid, one-size-fits-all. In 5,456 email triggers it produced 187 unique clicks (3.4%) and zero measurable return loan applications. The same refer-a-friend email runs twice with the same subject line. There are 88 days of silence between the first and second email. No SMS. No FHL cross-sell. No value content.

FHL has a documented 18-month lifecycle plan with real value at each touchpoint (Cotality valuations, repricing, refinance pathways). The plan is good. It is just not automated or connected to any system. So it does not happen.

The marketing function has a gap following Jared's resignation. Rowdie Lang manages operations and marketing with a custom GPT and a content engine pulling SEMrush, GA4, and Search Console.

### What Is Working

The sales process is strong. Once a lead gets on the phone with a FFG broker, 95%+ complete an application. 80%+ return documents. Approximately 30% are approved. Settlement rate after approval is 98%. This is not the gap.

Repeat and referral business accounts for 70-80% of FFG settlements. Brad (top broker) runs at 80% repeat/referral. The relationship-based model works.

Customer care calls generated 41 new enquiries last month with no automation at all.

Open rates on the existing post-settlement sequence sit at 41-74% per email. The brand is trusted. The relationship is real. It is the content and the structure that need rebuilding, not the audience. That is good news. We are not starting from zero.

### Group Financial Snapshot

| Metric | FFG | FHL | Combined |
|--------|-----|-----|----------|
| Leads per month | 375 | 55 | 430 |
| Settlements per month | 90-108 | 16-17 | 106-125 |
| Revenue per lead | ~$433 | ~$1,050 | - |
| Average deal value | $2,300 commission | $4,750-$5,225 income | - |
| Staff | 15 | Part of Fox team | ~33 total (incl. UMI ~18) |

Lead acquisition is 98% organic (primarily SEO-driven website traffic). Google Ads spend is $3,000 per month total ($1,500 FFG + $1,500 UMI) and FFG is net negative on paid.

49,000 leads per year are sent to the lead market (34,000 UMI, 15,000 Fox) and never re-engaged. Nathan estimates this pool is worth $1 million per year if properly reactivated.

1,050+ referral partner businesses sit in the database. Only 3-4 are actively referring.

---

## Strategic Direction: One Group, Built in GHL

### What We Are Building

Both master playbooks (Cross-Selling & Monetisation, and Pre-Sales SDR) ship through GoHighLevel. GHL handles about 80% of what Fox needs out of the box. Pipelines, nurture, SMS and email, tagging, lead scoring. Njin layers Claude and integrations on top for the other 20%. ICA routing. AI-personalised content. Behavioural branching that responds to what the customer actually does, not what the calendar says.

The custom POLR build is paused as of 16 April 2026 (Mati decision). Not killed. If GHL hits a real wall during build, the custom path is back on the table. For now, every dollar of build goes into GHL.

### The 5-ICA Post-Settlement Engine

The new system replaces the broken 6-email sequence with a 12-month, 12-touchpoint nurture program built around five ICA-specific journeys. Every customer is tagged at settlement and routed into the journey that fits their financial profile, life stage, and likely next need.

| Journey component | What it does |
|---|---|
| Master Entry Workflow | Triggered when `FFG_Settled` is applied. Reads ICA tag (YPMB / EPFB / PCLRB / BAB / PVB) and routes to the matching sub-workflow. Routing only - no content. |
| 5 ICA Sub-Workflows | One per ICA. Quarterly cadence (Day 3, 7, 30, 90, 180, 270, 365 + win-back). Email and SMS. ICA-specific subject lines, content, tone, FHL cross-sell timing. |
| Behavioural Branch Workflows | Triggered by tags applied from email clicks, SMS replies, or FHL content engagement. Pause the ICA workflow and route to the appropriate branch. |
| FHL Referral Workflow | Standalone 3-email FHL intro sequence. Triggered when any customer clicks FHL-related content. Runs in parallel, then returns the contact to the ICA workflow. |
| Broker Handoff Workflow | Triggered by `FFG_HotLead`. Sends an internal GHL task to the assigned broker, pauses the email sequence for 14 days while a human follows up. |

Every ICA journey ends with an FHL conversation. Cross-sell is not an add-on. It is built into the architecture from Day 3.

### The "Give It All Away" Philosophy

A broker earns a commission, says thanks, and waits for the client to come back. That is the old model. Transactional.

Here is the shift. Every client who enters the Fox ecosystem gets ongoing value before they are ever asked for the next loan:

- **Credit education** matched to where they are (first-time car loan vs prime repeat)
- **Property valuations** via Cotality, sent proactively to homeowners
- **Rate intelligence** at meaningful intervals (not noise, real movements)
- **Life-stage planning content** that anticipates their next financial need
- **Cross-entity introductions** at the right moment, not the obvious moment

This earns the right to sell. By Month 9, when the credit profile has rebuilt and the data shows a return loan is most likely, Fox has been in the customer's corner for 9 months. The "ready when you are" message lands instead of getting filed as spam.

### How the New System Changes the Client Relationship

| Before | After (GHL + 5-ICA Engine) |
|---|---|
| One loan, one commission, relationship ends | One entry point, FHL pathway in every journey, lifetime customer value |
| Cross-sell depends on broker memory | Behavioural triggers route customers to FHL the moment they show interest |
| Post-settlement nurture is generic emails | 12 ICA-specific touchpoints across email + SMS over 12 months |
| Non-converting leads are sold and forgotten | Reactivation campaign targets 6-12 month dormant leads (12-month tested first) |
| Three separate customer databases | One GHL view fed by Ambition CSV (FFG) + Infynity CSV (FHL) |
| Email opens are the engagement signal | Click-based triggers (iOS Mail Privacy Protection broke open-tracking reliability) |

### Technical Foundation

| Layer | Tool | Role |
|---|---|---|
| CRM + automation | GoHighLevel | Pipelines, workflows, tagging, scoring, email + SMS |
| Email content engine | Fox-MIS EDM Creator Agent | Drafts every email using ICA intelligence; reviewed before loading to GHL as a template |
| FFG data | Ambition (CSV export) | Source of truth for FFG settlements and ICA classification |
| FHL data | Infynity (CSV export, formerly Connective) | Source of truth for FHL pipeline and post-settlement data |
| UMI data | Proprietary CTO-built system | Direct UMI clients only; broker-referred UMI clients are quarantined from cross-sell |
| Property valuations | Cotality | 90-day pack, annual reviews, equity triggers; integrated to GHL |
| SMS | GHL native (Twilio backend) | Separate number, standard practice |
| Email (legacy) | SendGrid | Existing FFG sequence; access pathway being finalised by Xavier |

LMG (Lone Market Group) was evaluated as an Infynity replacement and is off the table (locked 27 April 2026).

---

## Related Documents

- Ideal Client Profiles and Avatars
- Business Model
- Pipeline Overview (pending)
- Customer Journey and Lifecycle (pending; will detail the 12-touchpoint quarterly cadence)
