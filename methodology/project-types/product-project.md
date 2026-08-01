# Project Type: Product Project (SaaS)

**What it is:** A SaaS product build or optimisation engagement. Used for internal Njin products (like AIpreneurs) or external SaaS clients needing growth strategy and execution.

---

## Framework Used
**JK Growth** — see `frameworks/jk-growth.md`.

---

## Phase Model
**5 Phases:** Discovery > Product Fundamentals > Launch Strategy > Execution > Scaling

---

## Typical Engagement Shape

| Attribute | Value |
|-----------|-------|
| **Duration** | 3-12 months depending on stage |
| **Deliverables** | ICP profile, Lean Canvas, growth engine plan, launch playbook, live campaigns, scaling roadmap |
| **Client time commitment** | 4-8 hours/week |
| **Pricing model** | Retainer or milestone-based |
| **Team involved** | PM, Growth specialists (PLG/ALG/CLG), Marketing, Sales, Product, Dev |

---

## Required COS Fields

```yaml
product:
  name, description, stage
  lean_canvas: {problem, solution, customer_segments, channels, revenue_streams, key_metrics}

twelve_core_numbers_saas:
  mrr, growth_rate, churn, ltv, cac, nrr, arpu
  trial_to_paid_conversion

growth_engine:
  selected: plg | alg | clg | hybrid
  rationale: [why this engine]

active_workstreams:
  - {name, owner, deadline, deliverables, status, notes}

launch_play:
  type, target_date, channels

qualitative_context:
  money_leak, twelve_month_goal, ninety_day_priority
  time_budget_warnings

phase:
  current: discovery | fundamentals | launch | execution | scaling
```

---

## What a "Correct" Plan Looks Like

1. **Lean Canvas complete** — problem, solution, customers, channels, revenue, metrics
2. **ICP clearly defined** — who buys and why
3. **Growth engine selected with rationale** — PLG, ALG, CLG, or hybrid
4. **12 Core Numbers logged** (SaaS version) — even if some are "unknown"
5. **Active workstreams tracked** — each with owner, deliverables, deadline
6. **90-day priority identified** — what matters most right now
7. **Time budget warnings flagged** — product work eats time, budget it explicitly

---

## Growth Engine Selection

| Engine | Best for |
|--------|----------|
| **PLG (Product-Led Growth)** | Self-serve products with quick time-to-value, freemium, viral loops |
| **ALG (AI-Led Growth)** | AI-native products, personalisation at scale, agent-driven experiences |
| **CLG (Community-Led Growth)** | Network effects, user-generated value, platform dynamics |
| **Hybrid** | Most mature products — combine 2-3 engines |

---

## Scoping Questions

1. What's the product, who's it for, and why does it exist?
2. What stage is the product at? (Idea, MVP, PMF, growth, scale)
3. What's your current MRR and growth rate?
4. What's your primary constraint — acquisition, activation, retention, or monetisation?
5. What growth experiments have you tried? What worked? What didn't?
6. Who's your ideal customer (ICP) — specific, not generic?
7. What's your pricing model and ARPU?
8. What's your CAC and LTV?
9. What does your current funnel look like?
10. What's your 12-month revenue target?

---

## Blocking Gates

1. **Voice Gate** — brand voice / ToV defined before any external content
2. **Data Access Gate** — analytics, metrics, customer data accessible
3. **Lean Canvas Complete** — before launch planning
4. **Growth Engine Selected** — before execution

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Building features without PMF | Validate demand before building |
| Choosing a growth engine without data | Diagnose the actual constraint first |
| Shiny object syndrome | Do more of what's working before trying new things |
| Treating AIpreneurs like a Njin Method engagement | AIpreneurs uses JK Growth, not TORQUE — different phase model |
| AIpreneurs tasks going to Notion | Critical rule: AIpreneurs tasks go to Reclaim + COS, never Notion |

---

## When This is the Right Project Type

- Client has a SaaS product (or is building one)
- Product has users or clear path to users
- Problem is growth-related, not delivery-related
- Client can commit time (SaaS growth is hands-on)

## When It's NOT the Right Project Type

- Client has no product yet (too early — coach them first)
- Client needs a service playbook (Njin Method)
- Client needs a website (AetherFlow)
- Client's real constraint is revenue extraction from existing customers, not growth (Njin Method retention playbook)

---

## Special Case: AIpreneurs

AIpreneurs is Njin's internal SaaS product and uses this project type. Key rules:
- **Tasks tracked in Reclaim + COS, NOT Notion**
- **AIpreneurs < > James Killick Co** for tasks where JKC delivers services to AIpreneurs
- Uses JK Growth methodology
- Currently in V2 re-architecture phase

---

**Source:** `docs/background/frameworks/jk-growth/`, `docs/background/product-framework/`, `docs/background/project-examples/` (product project examples).
