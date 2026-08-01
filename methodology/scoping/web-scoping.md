# Scoping Guide: Web Project (AetherFlow)

Use this guide for discovery and scoping of marketing websites, funnels, and dashboards.

---

## Required Documents (Before Scoping Starts)

- [ ] Signed contract or engagement letter
- [ ] Brief describing what the client wants
- [ ] Existing brand assets (logo, colours, fonts) if any
- [ ] Existing content if any
- [ ] Reference sites the client likes

---

## Project Type Definition

- [ ] **Type** — marketing website / landing page / sales funnel / web app / dashboard / hybrid
- [ ] **Primary goal** — leads / sales / brand / information / user engagement
- [ ] **Secondary goals** — ___

---

## Target Audience (ICP)

- [ ] **Who is this for?** (specific persona, not "anyone who needs X")
- [ ] **Demographics** — age, location, role
- [ ] **Pain points** — what problem brings them to the site?
- [ ] **Awareness stage** — unaware / problem-aware / solution-aware / product-aware
- [ ] **What do they care about?** — list 3-5 things
- [ ] **Competitors they'll compare to** — ___

---

## Content Strategy

- [ ] **Key messages** — what must visitors understand after 10 seconds?
- [ ] **Pages / sections needed** — ___
- [ ] **Content themes** — what topics does the content cover?
- [ ] **Content ownership** — does the client write it? Do we? Copywriter needed?
- [ ] **SEO priority** — new site / refresh / migration / none
- [ ] **Target keywords** — ___ (primary + secondary)

---

## Brand Identity

- [ ] **Logo** — exists / needs to be created
- [ ] **Colour palette** — defined / needs creation
- [ ] **Typography** — defined / needs selection
- [ ] **Tone of voice** — defined / needs to be extracted
- [ ] **Visual style** — modern / minimal / bold / traditional / playful / other
- [ ] **Reference sites** — 2-3 sites the client likes and why
- [ ] **Anti-references** — 1-2 sites the client doesn't want to look like

---

## Technical Scope

### Stack Preferences
- [ ] **Framework** — Vite/React / Next.js / Astro / WordPress / other
- [ ] **UI library** — shadcn/ui / custom / other
- [ ] **CMS** — headless / WordPress / none (content in code)
- [ ] **Hosting** — Vercel / Netlify / client's hosting / other
- [ ] **Domain** — client owns / needs to acquire
- [ ] **Analytics** — GA4 / Plausible / Fathom / other
- [ ] **Email capture** — Mailchimp / ConvertKit / GHL / other

### Integrations Required
- [ ] CRM integration — ___
- [ ] Email platform — ___
- [ ] Booking tool (if applicable) — ___
- [ ] Payment processing (if applicable) — ___
- [ ] Live chat — ___
- [ ] Analytics — ___

---

## Key Features / Pages

List all pages or features:

| Page/Feature | Type | Content ready? | Priority |
|--------------|------|----------------|----------|
| Home | Landing | No | Must-have |
| About | Content | Partial | Must-have |
| [Feature X] | Interactive | No | Should-have |

---

## Performance Targets

Required for QA gate:
- [ ] **LCP** (Largest Contentful Paint) — target <2.5s
- [ ] **INP** (Interaction to Next Paint) — target <200ms
- [ ] **CLS** (Cumulative Layout Shift) — target <0.1
- [ ] **Accessibility** — WCAG 2.1 AA
- [ ] **SEO** — meta tags, schema markup, sitemap, robots.txt

---

## Timeline & Budget

- [ ] **Launch date** — is there a hard deadline?
- [ ] **Budget** — total project cost
- [ ] **Content readiness** — when will content be ready?
- [ ] **Review cadence** — how often for client reviews?

---

## Post-Launch Plan

- [ ] **Who updates content?** — client / Njin retainer / other
- [ ] **Maintenance model** — retainer / ad-hoc / self-service
- [ ] **Analytics review cadence** — weekly / monthly / none

---

## Stepwise Implementation Agreement

AetherFlow enforces: Structure > Styling > Interactions > Logic. Confirm with client:

- [ ] Client understands pages will look "raw" in structure phase
- [ ] Client will wait for styling phase before judging visual design
- [ ] Client will provide feedback at each step

---

## Discovery Gaps Template

```markdown
## Gaps Identified

### Hard Blockers
- No brand assets and no budget for creation
- Content not started and no SME available to write it
- No hosting plan — infrastructure decision blocks development

### Nice-to-Haves
- Logo needs refresh — can launch with current, update later
- SEO audit of old site — helpful but not blocking
```

---

## Blocking Gates

1. **Strategy Approved** — ICP, content strategy, SEO plan, brand identity confirmed
2. **Structure Phase Complete** — before styling starts
3. **Styling Phase Complete** — before interactions
4. **Interactions Phase Complete** — before logic
5. **QA Passed** — accessibility, performance, cross-browser

---

**Source:** `docs/background/frameworks/aetherflow/`, AetherFlow methodology docs.
