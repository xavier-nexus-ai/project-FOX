# Scoping Guide: Product Project (SaaS)

Use this guide for discovery and scoping of SaaS product engagements.

---

## Required Documents (Before Scoping Starts)

- [ ] Signed contract or internal project brief
- [ ] Existing Lean Canvas (if any)
- [ ] Current metrics dashboard access
- [ ] Product roadmap (if any)

---

## Product Context

- [ ] **Product name** — ___
- [ ] **One-line description** — ___
- [ ] **Stage** — idea / MVP / PMF / growth / scale
- [ ] **Target market** — B2B / B2C / SMB / enterprise / hybrid
- [ ] **Core value proposition** — ___

---

## Lean Canvas (Must Complete)

Fill every field:

### 1. Problem
- Top 3 problems the product solves — ___

### 2. Customer Segments
- **Target customers** — ___ (specific, not "everyone")
- **Early adopters** — ___ (who buys first?)

### 3. Unique Value Proposition
- Single, clear message — ___
- High-level concept (X for Y) — ___

### 4. Solution
- Top 3 features that solve the problems — ___

### 5. Channels
- How does the product reach customers? — ___

### 6. Revenue Streams
- Pricing model — freemium / subscription / one-time / usage-based / hybrid
- Pricing tiers — ___

### 7. Cost Structure
- Customer acquisition cost — ___
- Distribution costs — ___
- Hosting and infrastructure — ___

### 8. Key Metrics
- What matters most? — ___

### 9. Unfair Advantage
- Something that can't be copied — ___

---

## The 12 Core Numbers (SaaS Version)

Collect all, even if some are "unknown":

1. **MRR (Monthly Recurring Revenue)** — $___
2. **Growth rate** — ___% MoM
3. **Churn rate** — ___% monthly
4. **LTV (Lifetime Value)** — $___
5. **CAC (Customer Acquisition Cost)** — $___
6. **LTV:CAC ratio** — ___
7. **NRR (Net Revenue Retention)** — ___%
8. **ARPU (Average Revenue Per User)** — $___
9. **Trial-to-paid conversion** — ___%
10. **Activation rate** — ___%
11. **Time to value** — ___ minutes/hours
12. **Total users** — ___

---

## Growth Engine Selection

Choose one or hybrid:

- [ ] **PLG (Product-Led Growth)** — self-serve, freemium, viral, quick time-to-value
- [ ] **ALG (AI-Led Growth)** — AI-native product experiences, personalisation at scale
- [ ] **CLG (Community-Led Growth)** — network effects, user-generated content, platform dynamics
- [ ] **Hybrid** — combine 2-3 engines

**Rationale for selection:** ___

---

## Current State Assessment

### What's Working
- [ ] ___
- [ ] ___

### What's Broken
- [ ] ___
- [ ] ___

### Biggest Constraint Right Now
- acquisition / activation / conversion / retention / monetisation / referral

### 90-Day Priority
- What's the single most important thing to fix or improve? ___

---

## Team & Resources

- [ ] **Team composition** — founders, engineers, designers, marketing, sales, support
- [ ] **Dev capacity** — hours/week available for growth work
- [ ] **Marketing budget** — $___/month
- [ ] **Tools in use** — analytics, CRM, email, support, product analytics

---

## Analytics & Data Access

Required for growth diagnosis:
- [ ] **Product analytics** — Mixpanel / Amplitude / PostHog / other
- [ ] **Web analytics** — GA4 / Plausible / other
- [ ] **Revenue analytics** — Stripe dashboard / Baremetrics / ChartMogul / other
- [ ] **Customer feedback** — NPS tool / support tickets / user interviews
- [ ] **CRM access** — ___

**Rule:** Cannot diagnose a growth problem without data. If analytics are broken, fix them first.

---

## Active Workstreams

Every active initiative gets tracked:

```yaml
active_workstreams:
  - name: [workstream name]
    owner: [who's running it]
    deadline: [target date]
    deliverables: [list]
    status: [not_started | in_progress | blocked | complete]
    notes: [context]
```

---

## Goals & Success Criteria

- [ ] **12-month revenue target** — $___
- [ ] **12-month user target** — ___
- [ ] **90-day milestone** — ___
- [ ] **Next critical milestone** — ___ (and date)

---

## Time Budget Warnings

- [ ] **Founder time available** — hours/week for growth work
- [ ] **Dev capacity for growth features** — hours/week
- [ ] **Marketing execution capacity** — can the team actually run campaigns?

**Flag if:** time budget doesn't support the goals. Better to know upfront.

---

## Special Rules for AIpreneurs

If this is AIpreneurs or another internal Njin product:
- [ ] **Tasks go to Reclaim + COS, NOT Notion** — this is a critical rule
- [ ] **Use JK Growth methodology, not TORQUE**
- [ ] **Phase model is Discovery > Fundamentals > Launch > Execution > Scaling**
- [ ] **Current phase must be tracked in COS**

---

## Discovery Gaps Template

```markdown
## Gaps Identified

### Hard Blockers
- Lean Canvas incomplete — cannot proceed to growth engine selection
- Analytics broken — cannot diagnose current constraint
- No ICP defined — can't build targeted growth strategy

### Nice-to-Haves
- Competitor analysis missing — will do in Discovery phase
- Customer interviews not scheduled — will do in Weeks 1-2
```

---

## Blocking Gates

1. **Voice Gate** — brand voice / ToV defined before external content
2. **Data Access Gate** — analytics, metrics, customer data accessible
3. **Lean Canvas Complete** — before launch planning
4. **Growth Engine Selected** — before execution phase

---

**Source:** `docs/background/frameworks/jk-growth/`, `docs/background/product-framework/`.
