# Scoping Guide: Vibe Coding Project

Use this guide when running discovery and scoping for a software development (VIBE OS) engagement.

---

## Required Documents (Before Scoping Starts)

- [ ] Signed contract or engagement letter
- [ ] Client brief or product idea
- [ ] Any existing designs, wireframes, or mockups
- [ ] Any existing code (if brownfield)

---

## Product Context

- [ ] **Product / project name** — ___
- [ ] **One-line description** — ___
- [ ] **Problem it solves** — ___
- [ ] **Target user** — ___ (be specific: role, context, frequency of use)
- [ ] **Core user workflow** — ___ (what do they do with it?)
- [ ] **Stage** — idea / prototype / MVP / beta / production / scale

---

## Scope Definition

### MVP Scope
- [ ] **What's the absolute minimum that proves value?**
- [ ] **What features are essential for the first usable version?**
- [ ] **What's explicitly out of scope for the MVP?**

### Feature List
For each feature:
- [ ] Name
- [ ] Priority (must-have / should-have / nice-to-have)
- [ ] User story: As a __, I want __, so that __
- [ ] Acceptance criteria

---

## Technical Scope

### Tech Stack Preferences
- [ ] **Frontend preference** — Next.js / React / Vite / Astro / other
- [ ] **Backend preference** — Next.js API routes / separate backend / serverless
- [ ] **Database** — Supabase / Postgres / MongoDB / other
- [ ] **Auth** — Clerk / Supabase Auth / Auth0 / custom
- [ ] **Billing** — Stripe / Paddle / other / none
- [ ] **Hosting** — Vercel / AWS / client's infrastructure

### Data Model
- [ ] **Core entities** — what are the main objects in the system?
- [ ] **Relationships** — how do entities relate?
- [ ] **Multi-tenancy** — single-tenant or multi-tenant?
- [ ] **Data volume** — estimate at MVP and at scale

### Integrations Required
- [ ] External APIs — ___
- [ ] Third-party services — ___
- [ ] Existing client systems — ___

---

## Team & Access

- [ ] **Who owns the codebase after launch?**
- [ ] **Who maintains it post-launch?**
- [ ] **Is there an existing dev team or just Njin?**
- [ ] **Repository access** — where does the code live?
- [ ] **Deployment access** — who can push to production?

---

## Non-Functional Requirements

- [ ] **Performance expectations** — target response times, Core Web Vitals if web
- [ ] **Scalability needs** — MVP users, 6-month users, 12-month users
- [ ] **Security requirements** — data sensitivity, compliance needs
- [ ] **Availability** — uptime requirements
- [ ] **Accessibility** — WCAG level required

---

## Timeline & Budget

- [ ] **Hard deadline** — is there one? What drives it?
- [ ] **Budget** — total or hourly rate?
- [ ] **Team availability** — full-time / part-time?
- [ ] **Review cadence** — how often does the client want to review progress?

---

## Required Documentation (Will Be Created)

- [ ] **PRD (Product Requirements Document)** — must be created before code
- [ ] **Architecture document** — system design, tech stack decisions
- [ ] **Data model** — entity relationships
- [ ] **API spec** — if building backend or integrations

---

## Stepwise Development Agreement

VIBE OS enforces stepwise development: Structure > Styling > Interactions > Logic. Confirm:

- [ ] Client understands and agrees to stepwise approach
- [ ] Client will not demand "finished looking" pages before all structure is in place
- [ ] Client will provide feedback at each step, not just at the end

---

## Brownfield Considerations (if existing codebase)

- [ ] **Current state** — working / partially working / broken
- [ ] **Code quality** — will there be significant rework?
- [ ] **Tech debt** — known issues to inherit
- [ ] **Existing team knowledge** — who knows this codebase?
- [ ] **Testing coverage** — existing tests?

---

## Discovery Gaps Template

```markdown
## Gaps Identified

### Hard Blockers
- No clear MVP scope — cannot estimate
- No design direction — structure phase blocked
- Data model not defined — architecture blocked

### Nice-to-Haves
- Integrations TBD — can be deferred to Phase 2
- Branding not final — styling phase has flexibility
```

---

## Blocking Gates

1. **PRD Approved** — before architecture
2. **Architecture Approved** — before story breakdown
3. **Stories Ready** — before development
4. **QA Passed** — before deployment

---

**Source:** `docs/background/frameworks/vibe-os/`, VIBE OS methodology docs.
