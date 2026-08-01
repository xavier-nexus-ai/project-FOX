# Project Type: Njin Method Client

**What it is:** A revenue-focused engagement targeting one or more of the 4 revenue pillars (Acquisition, Conversion, Monetisation, Retention). Delivered via 1-2 playbooks with CRM automation and team training.

---

## Framework Used
**Njin Method (TORQUE)** — see `frameworks/njin-method.md` for full framework reference.

---

## Phase Model
**TORQUE:** Transform > Observe > Roadmap > Qualify > Upgrade > Evolve

In practice, the internal delivery phases are:
1. Activation — Data Collection & Validation (Weeks 0-1)
2. Immersion & Tone of Voice (Weeks 1-2)
3. Methodology Creation / Playbook Draft (Weeks 2-3)
4. Strategic Presentation & Revision (Week 3)
5. CRM Implementation (Weeks 4-6)
6. Team Training (Weeks 7-8)
7. Live Monitoring (Weeks 9-12)
8. Handover to Customer Success (Week 12)
9. 30-Day and 90-Day Reviews (Day +30, +90)

---

## Typical Engagement Shape

| Attribute | Value |
|-----------|-------|
| **Duration** | 12 weeks active + 90-day review period |
| **Deliverables** | 1-2 playbooks, CRM automation, team training, before/after metrics |
| **Client time commitment** | ~2-5 hours/week |
| **Pricing model** | One-time playbook fee + optional ongoing retainer |
| **Typical deal size** | $5K-$50K+ depending on scope |
| **Team involved** | PM, Sales, Developer (CRM specialist), Trainer, Customer Success AM |

---

## Required COS Fields

```yaml
client:
  name, company, industry, revenue_model, team_size
  primary_offer, pricing_model, target_audience

core_12:
  revenue_last_12_months, revenue_prior_12_months
  leads_per_month, cost_per_lead
  lead_to_appointment_rate, show_rate, close_rate, average_deal_size
  mrr_or_contract_length, churn_or_lifespan, customer_ltv, cac

constraint_diagnosis:
  primary_constraint: acquisition | conversion | monetisation | retention
  secondary_constraint: [same options]
  rationale: [why this diagnosis]
  ninety_day_priority: [from qualitative question 4]

qualitative_answers:
  money_leak: [answer]
  twelve_month_goal: [answer]
  next_revenue_milestone: [answer + date]
  ninety_day_fix: [answer]

tone_of_voice:
  created: true/false
  approved: true/false
  path: [link to guide]

data_access:
  crm_access_granted: yes/no
  historical_data_received: yes/no
  team_interviews_scheduled: yes/no
  shared_folder_populated: yes/no

playbooks:
  - type: [outreach | ads | pre-sales | sales | cross-sell | referral | retention]
    status: [draft | review | final | implementing | live]
    path: [link]
```

---

## What a "Correct" Plan Looks Like

A correct Njin Method project plan has:

1. **The Core 12 collected and logged** (even if some values are "unknown" — must be explicit)
2. **A constraint diagnosis** with primary, secondary, rationale, and 90-day priority
3. **The right playbook(s) selected** based on the constraint — not random playbooks
4. **Tone of Voice gate cleared** before any copy is generated
5. **CRM implementation phase planned** with dev resourcing confirmed
6. **Team training phase scheduled** with client availability confirmed
7. **Before-snapshot metrics captured** for the 90-day after comparison

---

## What Makes a Plan INCORRECT

These are the failure modes — what Michael's Avanti plan did wrong:

- ❌ Plan created from the proposal alone, without framework consultation
- ❌ Core 12 not collected before playbook work started
- ❌ Constraint diagnosis missing or hand-waved
- ❌ Playbook type chosen without aligning to constraint
- ❌ Tone of Voice skipped or deferred until after copy is written
- ❌ CRM implementation scoped without dev team input
- ❌ No "Earliest Possible Win" defined

---

## Typical Scoping Questions

Use the `scoping/njin-scoping.md` guide for the full intake. Key questions:

1. What's your revenue for the last 12 months?
2. What's your lead flow (leads/month)?
3. What's your conversion rate from lead to customer?
4. What's your average deal size and customer LTV?
5. Where do you think you're leaking the most money right now?
6. What's your 12-month revenue goal?
7. What would be the "Earliest Possible Win" if we started tomorrow?
8. Do you have a CRM? Which one? Who has admin access?
9. Do you have existing scripts, brand guidelines, or tone of voice docs?
10. Who on your team would own the outcome of this playbook?

---

## Blocking Gates (in order)

1. **Contract Gate** — signed contract, payment confirmed
2. **Data Access Gate** — CRM access, historical data, team interviews, Core 12 logged
3. **Tone of Voice Gate** — ToV guide created and client-approved
4. **Baseline Validated Gate** — Core 12 confirmed accurate with client
5. **Internal Review Gate** — playbook draft passes internal review
6. **Client Sign-off Gate** — client has formally approved the playbook
7. **Go-Live Gate** — pre-launch checklist 100% complete, team trained

---

## Common Pitfalls

| Pitfall | How to avoid |
|---------|--------------|
| Starting playbook before Core 12 is logged | Enforce Data Access Gate |
| Generic playbook content | Reference Core 12 and constraint in every section, document-level |
| Client not using the playbook after delivery | Ensure Team Training phase delivers certified users, not just a workshop |
| Metrics not tracked post-go-live | Active Monitoring phase has weekly check-in — don't skip it |
| No upsell at phase completion | Every closure produces a Next-Stage Proposal (Ascension/Selling/Reselling) |

---

## When This is the Right Project Type

- Client's problem is clearly revenue-related (leads, conversion, LTV, churn)
- Client has an existing sales/marketing operation that needs systematising
- Client wants measurable before/after results in 90 days
- Client has a CRM (or is willing to adopt one)
- Budget fits the typical range

## When It's NOT the Right Project Type

- Client has no existing IP or methodology (consider AI Orchestration)
- Client needs software built, not a playbook (consider VIBE OS)
- Client needs a new website, not CRM work (consider AetherFlow)
- Client's problem is product-market fit, not execution (coach them first)

---

**Source:** `docs/background/frameworks/njin-method/`, `docs/background/playbook-creation-sop.md`, `docs/ip-vault/delivery-sequences/ds-002-playbook-delivery.md`.
