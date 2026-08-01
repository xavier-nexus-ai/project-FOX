# Framework Reference: AetherFlow

## Purpose

AetherFlow is a full-service digital agency framework for building and launching digital projects — websites, funnels, dashboards, blogs, and interactive platforms. It runs a structured multi-agent workflow through research, strategy, build, and release, with TORQUE-style phase management and enforced context handoffs between roles.

## Target Audience

Clients who need a digital presence built, improved, or launched. Fits when:

- The deliverable is a website, marketing site, conversion funnel, or data dashboard
- The project needs research and strategy before build (not just execution)
- SEO, GEO (Generative Engine Optimisation), and content quality are part of the brief
- The client wants a complete, launch-ready digital asset — not just a dev task

Client signals that fit AetherFlow:
- "We need a new website"
- "We want to launch a funnel"
- "We need an analytics dashboard"
- "Our site isn't converting / ranking / getting found"
- "We're launching a new brand or product and need a web presence"

## Phases / Methodology

AetherFlow runs four sequential phases. Phase selection depends on the project scenario chosen at init.

**Foundation**
Research and positioning work. Covers competitor analysis, ideal customer profile (ICP) definition, and brand identity. Outputs a website or project specification ready for strategy.

**Strategy**
SEO and content strategy. Covers keyword research, technical SEO foundation, GEO strategy (for AI search visibility), sitemap generation, content strategy, offer and lead magnet design, and third-party integration planning.

**Implementation**
The build phase — stepwise development enforced in four sub-phases: UI Structure → UI Styling → Local Interactions → Core Functionality. The tech stack depends on the scenario selected (Astro for static sites, Next.js + Supabase for full platforms, Lovable/Vite for prototypes). No skipping phases. Agents cannot blend styling and functionality work.

**Testing & Deploy**
CI/CD setup, quality gate validation, accessibility and performance checks, and production release.

### Project Scenarios

Three scenario tracks determine the tech stack and which agents activate:

| Scenario | Use Case | Stack |
|----------|----------|-------|
| 1 — Proposals & Prototypes | Client demos, rapid MVPs | Lovable + Vite |
| 2 — Static Websites | Marketing sites, portfolios | Astro + Tailwind + shadcn/ui |
| 3 — Full Interactive Platforms | CMS, dashboards, AI tools, blogs | Next.js + Supabase + PGVector |

Modules (website, blog, funnel, quiz, dashboard) are selected within a scenario to define scope precisely.

## Key Deliverables

- Competitor analysis
- ICP document
- Brand identity guide
- Website or platform specification
- Keyword strategy
- Technical SEO foundation (robots.txt, sitemap, schema markup)
- GEO strategy (llms.txt, Answer Capsules, AI citation structure)
- Content strategy and pillar plan
- Offer and lead magnet document
- Integrations plan
- Fully built and styled website, funnel, or platform
- QA report and accessibility audit
- CI/CD pipeline (`.github/workflows/ci.yml`)

## Blocking Gates

- **Foundation Quality Gate** — Competitor analysis, ICP, brand identity, and website spec must all exist before entering Strategy. `foundation-quality` checklist must pass.
- **Strategy Quality Gate** — SEO checklist must pass before Implementation starts. Keyword strategy, technical SEO, and GEO strategy must be complete.
- **Implementation Phase Gate** — Each of the four build sub-phases must finish before the next begins. Orchestrator (Orion) enforces no phase skipping and intervenes if scope bleeds between phases.
- **40% Context Rule** — Not a hard block but a critical operating constraint. Agents must save progress and hand off when context reaches 60% used. Context loss kills momentum. Handoffs are mandatory at role switches.
- **Release Gate** — `release` checklist must pass before deployment. Includes Core Web Vitals, WCAG 2.1 AA, performance benchmarks, and brand consistency.

## Key Agents

| Agent | Name | Role |
|-------|------|------|
| **Orchestrator** | Orion | Project driver — startup checks, phase management, routes work, context health monitoring |
| **Initialization Agent** | Genesis | One-time setup — creates COS, deploys agents and skills, asks about scenario and modules |
| **Marketing Research** | Leo | Competitor analysis, ICP, brand identity, digital PR opportunities |
| **Business Analyst** | Chloe | Website and platform specs, accessibility requirements, acceptance criteria |
| **SEO Specialist** | Seraphina | Keywords, technical SEO, GEO strategy, GA4 AI referral setup, sitemap |
| **Content Strategist** | Arthur | Content pillars, tone of voice, blog briefs, Answer Capsules, MDX implementation |
| **Web Developer** | Jimmy | Builds in Astro (Scenario 2), Next.js (Scenario 3), or Lovable (Scenario 1) |
| **Funnel Developer** | Nova | Conversion funnels, quiz logic, A/B testing |
| **Dashboard Developer** | Atlas | BI dashboards, customer portals, realtime data (Next.js) |
| **UX/UI Designer** | Luna | Wireframes, design systems, component design |
| **QA Tester** | Quinn | Testing, accessibility validation, performance benchmarking |
| **CRO Specialist** | Marcus | Conversion audits and testing plans |
| **Data Specialist** | Isabelle | Schema, Supabase/PGVector setup, third-party integrations, API connections |
| **Proposal Creator** | Vivian | Interactive client proposals, prospect demos, pricing |
| **Product Specialist** | Alex | Product strategy, feature prioritisation |
| **Project Manager** | Jordan | Project coordination, stakeholder communication |

## Typical Engagement Shape

- **Duration:** Scenario 1 (proposals/prototypes) — days. Scenario 2 (static sites) — 1 to 3 weeks. Scenario 3 (full platforms) — 3 to 8 weeks depending on module count and complexity.
- **Client time commitment:** Medium. Required at Foundation review (approve ICP and brief), Strategy review (approve SEO and content direction), Implementation milestone reviews, and final QA sign-off.
- **Pricing model:** Project-based. Scenario and module selection drive scope. SEO and GEO strategy can be standalone or bundled.
- **Team involved:** Typically Orchestrator + relevant specialists per phase. Not all 16 agents activate on every project — scenario and module selection determines which agents are in scope.

## How to Scope This Framework

A PM needs the following before scoping an AetherFlow engagement:

**Must-have inputs:**
- What is the deliverable? (website, funnel, dashboard, platform, or proposal)
- Which scenario fits? (1 = prototype, 2 = static site, 3 = full platform)
- Which modules are in scope? (website, blog, funnel, quiz, dashboard)
- Does the client have brand assets, tone of voice, or existing style guide?
- Does existing content or copy exist, or is it being created from scratch?
- What integrations are required? (CRM, email platform, analytics, booking tools)
- Is SEO a priority, and is GEO (AI search visibility) in scope?

**Scope questions to ask:**
- How many pages are in scope for the initial build?
- Does the client need a design first, or are they working from an existing design?
- What's the hosting/deployment environment? (Vercel, Netlify, self-hosted)
- Is this a new build or a rearchitecture of something that already exists?
- What analytics are required at launch?

**Common missing-info pitfalls:**
- Scenario not confirmed early — this blocks tech stack selection and agent activation
- No brand guide or tone of voice document — content and design stall without it
- Integration requirements surface late — especially CRM connections or payment gateways
- Client expects SEO results immediately — set expectations around GEO indexing timelines
- Module scope creep — client adds quiz + blog + funnel after Foundation has already scoped for website only

## Signals This is the Right Framework

- The deliverable is a website, funnel, dashboard, or digital platform
- Research and strategy need to precede the build
- SEO and AI search visibility are part of the brief
- The client needs a launch-ready asset, not just a dev task
- Content quality and conversion are requirements, not afterthoughts
- The project has defined scope (scenario + modules) or can be defined in discovery

## Signals This is NOT the Right Framework

- The deliverable is a software product or SaaS application — use VIBE OS instead
- The client needs growth strategy for an existing SaaS — use JK Growth instead
- There is no web component — pure marketing strategy or campaign work doesn't need AetherFlow
- The project is an enterprise software build with complex architecture — VIBE OS is the right fit

## Source Materials

- `/docs/background/frameworks/aetherflow/README.md` — Overview, scenarios, agent roster, and CLI helpers
- `/docs/background/frameworks/aetherflow/CLAUDE.md` — Framework conventions and agent categories
- `/docs/background/frameworks/aetherflow/workflows/foundation.yml` — Foundation phase sequence
- `/docs/background/frameworks/aetherflow/workflows/strategy.yml` — Strategy phase sequence
- `/docs/background/frameworks/aetherflow/workflows/implementation.yml` — Implementation phase with sub-phase enforcement
- `/docs/background/frameworks/aetherflow/workflows/testing_deploy.yml` — Release phase
- `/docs/background/frameworks/aetherflow/agents/` — All 16 agent definitions
- `/docs/background/frameworks/aetherflow/docs/AetherFlow.md` — Core methodology reference
