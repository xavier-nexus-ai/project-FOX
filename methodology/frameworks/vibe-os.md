# Framework Reference: VIBE OS

## Purpose

VIBE OS is a natural language-first AI agent framework for the full software development lifecycle. It gives structured, stepwise direction to specialised AI agents — handling planning, architecture, implementation, testing, and project management — so software gets built predictably and to a maintainable standard.

## Target Audience

Software projects where AI agents are doing the heavy lifting across multiple development roles. Fits best when:

- A client needs a web app, SaaS product, or internal tool built
- The team wants AI to act as developer, architect, PM, and QA simultaneously
- The build requires governance and quality checkpoints, not just "vibe and ship"
- There is a clear product spec (PRD) or the team needs help producing one before building

Client signals that fit VIBE OS:
- "We need to build [software product]"
- "We have a spec but no dev team"
- "We want AI to help us build this"
- Enterprise or mid-market teams wanting structured AI-assisted development with oversight

## Phases / Methodology

VIBE OS organises work through the B.L.A.S.T. development workflow, with four enforced implementation sub-phases:

**Blueprint (Context Acquisition & Analysis)**
Read all project standards, gather requirements, define data schemas and the "north star" before writing any code.

**Link (Verification & Handshake)**
Verify all API connections and environment credentials. Work stops here if any connection is broken — nothing proceeds on assumptions.

**Architect (Planning & 3-Layer Execution)**
Produce a technical design across three layers: Architecture (SOP in docs), Navigation (decision routing), and Tools/Execution (deterministic code). Client approves the implementation plan before build starts.

**Implementation — 4 Enforced Sub-Phases**
1. UI Structure — Layout, routing, component hierarchy only. No styling, no interactions, no backend.
2. UI Styling — Branding, responsive design, visual polish only. No interactions or state.
3. Local Interactions — Client-side behaviours, animations, form validation only. No backend calls.
4. Core Functionality — Database, authentication, external APIs, AI features only. No new UI.

**Stylize & Trigger (Verification & Clean-up)**
Run build checks and unit tests. Apply Self-Annealing: if an error occurred, update the architecture docs to prevent the same error from ever recurring. Produce a walkthrough document.

## Key Deliverables

- Product Requirements Document (PRD) — if not provided, PM agent produces it
- Architecture design document
- Implementation plan (approved before build)
- Working codebase with structured components, pages, types, and services
- Unit and integration tests
- Walkthrough documentation of completed work
- CI/CD pipeline configuration
- Handoff documents between each agent role

## Blocking Gates

- **Link Gate** — All API connections and credentials must be verified before moving to Architect. Broken link = stop.
- **PRD Completeness Gate** — PM checklist must pass (or be near-pass) before architecture begins. Blockers must be resolved.
- **Plan Approval Gate** — Client must approve the implementation plan before any code is written.
- **Phase Enforcement** — Each of the four implementation sub-phases must complete before the next starts. No skipping. Orchestrator intervenes if an agent tries to cross phases.
- **File Size Gate** — Components capped at 300 lines, pages at 500 lines, utilities at 200 lines. Violations trigger refactoring before proceeding.
- **QA Gate** — All tests must pass and accessibility + performance checklists must clear before deployment.

## Key Agents

| Agent | Role |
|-------|------|
| **Orchestrator** | Startup checks, routes work, enforces phase discipline, monitors context health |
| **Initialization Agent** | One-time project setup — generates COS, CLAUDE.md, scaffolds structure |
| **Business Analyst** | Requirements gathering, market research, discovery |
| **Product Manager (PM)** | PRD creation, epic and user story definition, MVP scope validation |
| **Product Owner** | Feature prioritisation, roadmap, acceptance criteria |
| **Scrum Master** | Sprint planning, backlog management, velocity tracking |
| **Architect** | System design, technology selection, integration strategy, security architecture |
| **Lead Dev** | Senior implementation, code review, technical standards enforcement |
| **Dev** | Feature implementation, unit testing, iterative development |
| **QA Tester** | Testing, accessibility validation, performance benchmarking |
| **UI/UX Expert** | Wireframes, design systems, component design |
| **Coach** | Framework methodology training for the team |

## Typical Engagement Shape

- **Duration:** Days to months depending on project size. Rapid prototypes in days; enterprise builds in weeks to months.
- **Client time commitment:** Low to medium. Required at plan approval, milestone reviews, and stakeholder check-ins. Not involved in day-to-day execution.
- **Pricing model:** Project-based. Scope drives price — defined by phase count, feature complexity, and team configuration.
- **Team involved:** Typically PM/BA to define scope, Architect for system design, Dev for implementation, QA for validation. Enterprise projects add Scrum Master and separate Lead Dev.

## How to Scope This Framework

A PM needs the following before scoping a VIBE OS engagement:

**Must-have inputs:**
- What are we building? (web app, SaaS, internal tool, API, dashboard)
- Does a PRD or brief exist, or does the PM need to produce it first?
- What tech stack is preferred or already in use?
- What integrations are required? (third-party APIs, databases, auth providers)
- What are the non-functional requirements? (performance, security, compliance, accessibility)
- Who is approving the architecture and implementation plan?

**Scope questions to ask:**
- How many pages/features/user flows are in scope for the MVP?
- Is this greenfield or building on top of existing code?
- What does "done" look like — shipped to production, or handed to internal dev team?
- Is there an existing design system or brand guide?

**Common missing-info pitfalls:**
- Assuming the PRD is complete when it's a rough brief — always validate against the PM checklist
- No clarity on who can approve the architecture plan — this blocks the build starting
- Integration requirements discovered late (e.g., "it needs to connect to Salesforce") — always ask up front
- Client expects a working product but has no test environment or hosting plan

## Signals This is the Right Framework

- The deliverable is software — a web app, SaaS product, dashboard, or internal tool
- The client wants or is open to AI doing the heavy lifting across dev roles
- Quality, maintainability, and documentation matter — not just "get it done"
- There is a defined or definable spec before build starts
- The client needs governance and phase-by-phase progress tracking
- The project has complexity requiring architecture planning (not just a landing page)

## Signals This is NOT the Right Framework

- The deliverable is a marketing website or landing page — use AetherFlow instead
- The client just wants a quick proposal or prototype demo — AetherFlow Scenario 1 fits better
- There is no product spec and the client can't commit time to define one — not ready for VIBE OS
- The project is pure growth strategy, not software build — use JK Growth instead
- The client needs ongoing content, SEO, or conversion work — that's AetherFlow territory

## Source Materials

- `/docs/background/frameworks/vibe-os/README.md` — Overview and key concepts
- `/docs/background/frameworks/vibe-os/CLAUDE.md` — Agent roster and development conventions
- `/docs/background/frameworks/vibe-os/workflows/vibe-os-development.md` — B.L.A.S.T. workflow detail
- `/docs/background/frameworks/vibe-os/workflows/specification-driven/enterprise-project.yaml` — Enterprise project phase model
- `/docs/background/frameworks/vibe-os/checklists/pm-checklist.md` — PM validation checklist
- `/docs/background/frameworks/vibe-os/agents/` — All 12 agent definitions
