# Project Type: AI Orchestration Client (90-Day Build)

**What it is:** A 90-day engagement that extracts a client's intellectual property and turns it into a custom AI framework they own permanently. Used for consultancies, agencies, educators, and professional services firms who want to systematise their delivery.

---

## Framework Used
**AI Orchestration (AI Orchestrator Builder)** — see `frameworks/ai-orchestration.md` for full framework reference.

---

## Phase Model
**Immersion > Mapping > Transformation**

In practice:
1. Pre-engagement (Week 0): Sales handover, kick-off, COS creation
2. Immersion (Weeks 1-4): AI literacy, industry analysis, stack config, quick win
3. Mapping (Weeks 5-8): Workflow mapping, IP extraction, methodology naming, diagnostics, constraints, leverage
4. Transformation (Weeks 9-12): Framework construction, QA, deployment

---

## Typical Engagement Shape

| Attribute | Value |
|-----------|-------|
| **Duration** | 12 weeks (90 days) |
| **Deliverables** | 10 core deliverables (named methodology, diagnostics, playbooks, templates, agents, skills, workflows, tasks, COS, deploy script + scaling roadmap) |
| **Client time commitment** | 4-6 hours/week (peaks Weeks 5-6 at 6+ hours for IP extraction) |
| **Pricing model** | Fixed 90-day program fee, typically $13,500-$50,000+ |
| **Typical deal size** | $13.5K entry (SOLVD example) to $50K+ for complex engagements |
| **Team involved** | Delivery Lead (James for technical complexity, George for methodology-heavy), PM, potentially dev team for integration |

---

## Required COS Fields

```yaml
client:
  name, company, industry, business_model
  annual_revenue, team_size, team_composition
  primary_offer, pricing_model, delivery_model
  target_audience, framework_goals

business_health:
  annual_revenue, revenue_model, active_clients
  hours_per_client, founder_delivery_hours_per_week
  revenue_per_founder_hour, max_capacity
  leads_per_month, lead_to_client_conversion_rate
  average_engagement_value, client_lifetime_value
  biggest_revenue_leak, one_thing_to_systematise
  demand_vs_supply, twelve_month_revenue_goal, ninety_day_fix

phase:
  current: immersion | mapping | transformation
  immersion:
    status, started, completed
    deliverables: {ai_literacy, ai_possibilities_map, industry_report, stack_configured, vibe_coded_win}
  mapping:
    status, started, completed
    deliverables: {workflow_map, ip_vault_frameworks, ip_vault_sops, ip_vault_judgement_calls, ip_vault_vocabulary, ip_vault_delivery_sequences, methodology_named, methodology_structured, diagnostics_designed, constraint_map, leverage_plan}
  transformation:
    status, started, completed
    deliverables: {agents_built, skills_built, templates_built, workflows_built, cos_designed, assembled, qa_passed, deployed}

ip_vault:
  total_frameworks, total_sops, total_judgement_calls
  total_vocabulary_terms, total_delivery_sequences
  source_materials: [list]
  named_methodology: {name, tagline, phases}

framework_build:
  agents: {planned, built, list}
  skills: {planned, built, list}
  templates: {planned, built}
  workflows: {planned, built}
  cos_schema: {designed, path}
  deploy_script: {created, path}

gates:
  immersion_complete, ip_extraction_complete
  components_built, qa_passed, tone_of_voice
```

---

## What a "Correct" Plan Looks Like

1. **All source materials catalogued** in `ip_vault.source_materials` with processed status
2. **Immersion deliverables scheduled** — AI literacy sessions, industry analysis, stack config, quick win build
3. **Mapping sequence respected** — IP Extraction MUST complete before Methodology Architecture, before Diagnostics/Constraints/Leverage
4. **Minimum IP extraction targets** — 2+ frameworks, 3+ SOPs, 5+ judgement calls
5. **Methodology naming workshop scheduled** — 3-5 options presented, client picks
6. **Transformation build sequence documented** — COS > Architecture > Agents > Skills > Methodology Wiring > Diagnostics > Playbooks > Gates > Deploy Script > CLAUDE.md
7. **QA validation phase scheduled** — 10 validation categories
8. **First deployment plan** — which customer gets the framework deployed first in Week 12

---

## Critical Dependency Chain (Mapping Phase)

```
IP Extraction (Weeks 5-6) [MUST complete first]
    v
Methodology Architecture (Weeks 6-7)
    v
Diagnostics Design (Week 7) + Constraint Mapping (Weeks 7-8) [parallel]
    v
Leverage Planning (Weeks 7-8)
```

**You cannot structure what you haven't extracted.** This dependency is non-negotiable.

---

## Typical Scoping Questions

Use `scoping/orchestration-scoping.md` for the full intake. Key questions:

1. What intellectual property do you already have? (courses, frameworks, SOPs, methodologies, playbooks)
2. How do you currently deliver your service? Walk me through a typical client journey.
3. What's your delivery capacity — how many clients can you take on at once?
4. Where are you the bottleneck in your delivery? Where do things break?
5. What's your 90-day business goal?
6. What would it look like if AI could handle 50% of your delivery?
7. Who on your team currently does the work you want to systematise?
8. Do you have existing customer feedback, case studies, or success stories?
9. What tools and platforms are you already using?
10. Are you willing to commit 4-6 hours/week for 12 weeks?

---

## Blocking Gates (in order)

1. **Contract Gate** — signed contract, payment confirmed
2. **Immersion Complete** — AI literacy confirmed, AI Possibilities Map done, Industry Report done, stack configured, quick win built
3. **IP Extraction Complete** — 2+ frameworks, 3+ SOPs, 5+ judgement calls, methodology named
4. **Mapping Complete** — methodology structured, diagnostics designed, constraint map, leverage plan
5. **Components Built** — all 10 components complete
6. **QA Passed** — all 10 validation categories green
7. **Deployment Ready** — deploy script tested, client trained

---

## Common Pitfalls

| Pitfall | How to avoid |
|---------|--------------|
| Shallow IP extraction | Budget 3-5 interview sessions, use the DEPTH model |
| Generic framework output | QA checks IP fidelity specifically — flag if agents sound generic |
| Methodology naming stalls | Present 3-5 options with rationale, set a decision deadline |
| Scope creep in Mapping | Hit minimum extraction counts, note additional items for post-engagement |
| Week 12 crunch | Gates prevent this — if Immersion runs to Week 5, Mapping starts late and something compresses |
| Client treating it as a product purchase | Set expectations early: this is a co-creation, not a handover |

---

## Client Time Commitment by Week

| Week | Hours | Activity |
|------|-------|----------|
| 0 | 1 | Kick-off |
| 1-2 | 2-3/week | AI literacy sessions |
| 3 | 2 | Industry analysis review |
| 4 | 2-4 | Stack config + quick win build |
| 5-6 | 6-10 total | IP extraction (peak effort) |
| 7 | 1-2 | Methodology naming decision, diagnostics review |
| 8 | 1-2 | Constraint map + leverage plan review |
| 9-11 | 1-2/week | Framework component reviews |
| 12 | 3-5 | Training + first deployment |

**Total client commitment:** ~35-50 hours across 12 weeks.

---

## When This is the Right Project Type

- Client has existing IP (methodologies, frameworks, SOPs, processes)
- Client delivers a service that's repeatable but not yet systematised
- Client wants to scale delivery without proportionally scaling headcount
- Client has time to commit (4-6h/week for 12 weeks)
- Client is technically comfortable enough to learn Claude Code
- Client has revenue to support the engagement ($13K+ typical floor)

## When It's NOT the Right Project Type

- Client has zero existing IP — there's nothing to extract (run TORQUE first)
- Client is expecting a product purchase, not a co-creation
- Client can't commit the weekly time
- Client's primary need is revenue generation, not delivery systematisation (Njin Method instead)
- Client needs software built, not a framework (VIBE OS instead)

---

## Post-Engagement

After 90 days, the client's project folder becomes their **Master Project** — a permanent workspace where they iterate, improve, and extend the framework. Support options:
- Retainer (ongoing framework improvements, new agents, troubleshooting)
- Ad-hoc (pay-per-session for specific improvements)
- Self-service (training in Week 12 covers this)

---

**Source:** `docs/background/frameworks/ai-orchestration/`, `docs/background/sop-ai-transformation.md`, `docs/ip-vault/delivery-sequences/ds-003-ai-transformation-delivery.md`.
