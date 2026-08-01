# Project Type: Web Project

**What it is:** A marketing website, landing page, conversion funnel, or web dashboard. Delivered via AetherFlow — Njin's digital agency framework.

---

## Framework Used
**AetherFlow** — see `frameworks/aetherflow.md`.

---

## Phase Model
**TORQUE-style (4 phases):** Foundation > Strategy > Implementation > Testing & Deployment

With stepwise implementation: Structure > Styling > Interactions > Logic

---

## Typical Engagement Shape

| Attribute | Value |
|-----------|-------|
| **Duration** | 2-8 weeks for marketing sites, longer for funnels/dashboards |
| **Deliverables** | Deployed website/funnel/dashboard, content, SEO, analytics setup |
| **Client time commitment** | 2-5 hours/week for reviews and content |
| **Pricing model** | Fixed-price per project, or retainer for ongoing updates |
| **Team involved** | PM, Research/Content, SEO, Designer, Developer, QA |

---

## Required COS Fields

```yaml
project:
  name, type [website | funnel | dashboard]
  target_audience, primary_goal

brand_identity:
  visual_direction, typography, colour_system, logo
  tone_of_voice, key_brand_words

content_strategy:
  themes, purpose, distribution_plan

tech_stack:
  framework [Vite/React | Next.js | Astro]
  ui_library [shadcn/ui]
  state_management [React Query]
  forms [React Hook Form + Zod]
  hosting, ports

key_features:
  - {name, status, phase}

performance_targets:
  lcp, inp, cls, accessibility, seo

phase:
  current: foundation | strategy | implementation | testing | launch
  implementation_step: structure | styling | interactions | logic
```

---

## What a "Correct" Plan Looks Like

1. **ICP defined** — who is this for, what do they care about
2. **Content strategy approved** — themes, pages, SEO keywords
3. **Brand identity locked** — colours, typography, voice
4. **Information architecture mapped** — pages, navigation, user flow
5. **Stepwise implementation plan** — structure first, styling second, interactions third, logic fourth
6. **Performance targets set** — Core Web Vitals, accessibility, SEO
7. **Deployment plan** — hosting, domain, analytics, monitoring

---

## Scoping Questions

1. What's the goal of this site/funnel/dashboard? (Leads, sales, information, brand)
2. Who's the target audience? (ICP definition)
3. What pages/sections do you need?
4. Do you have existing brand assets (logo, colours, fonts)? If not, do we create them?
5. What's the CMS/content strategy — who updates this post-launch?
6. What integrations are needed? (CRM, email, analytics, booking)
7. What's the hosting plan?
8. SEO priority? (New site vs refresh vs migration)
9. Do you have existing content, or do we write it?
10. What's the deadline and budget?

---

## Blocking Gates

1. **Strategy Approved** — ICP, content strategy, SEO plan, brand identity confirmed
2. **Phase Complete** — each stepwise phase (Structure > Styling > Interactions > Logic) complete before next starts
3. **QA Passed** — accessibility (WCAG 2.1 AA), performance (Core Web Vitals), cross-browser tested

---

## Stepwise Implementation Rule

**Critical:** Don't jump phases. Build all structure first, THEN all styling, THEN all interactions, THEN all logic. This is not optional — it's the AetherFlow discipline.

Benefits:
- Structure is locked before styling distracts
- Styling is consistent across all pages
- Interactions are predictable
- Logic errors are easier to isolate

---

## Common Pitfalls

- Starting styling before structure is complete on all pages
- Content written after design (content should lead)
- SEO added as an afterthought (bake it in from the strategy phase)
- Accessibility ignored until launch (WCAG is a gate, not a nice-to-have)
- Missing Core Web Vitals targets (performance gets checked, not assumed)

---

## When This is the Right Project Type

- Client needs a website, funnel, or web dashboard
- Content and design can be scoped upfront
- Timeline is reasonable (not a week-before-launch panic)
- Client has brand assets or is willing to create them

## When It's NOT the Right Project Type

- Client needs a full web app (VIBE OS)
- Client needs CRM automation (Njin Method)
- Client has no content and expects Njin to write all of it without SME input
- Client wants cheap, fast, and good — pick two

---

**Source:** `docs/background/frameworks/aetherflow/`, `docs/background/project-examples/` (web project examples).
