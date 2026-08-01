# Project Type: Vibe Coding Project

**What it is:** A software development engagement — web apps, internal tools, dashboards, automation platforms, or product builds. Uses VIBE OS as the delivery framework.

---

## Framework Used
**VIBE OS** — see `frameworks/vibe-os.md`.

---

## Phase Model
Workflow-driven (not phase-gated like Njin Method):
1. **Discovery** — Requirements gathering, user stories
2. **Requirements** — PRD creation
3. **Architecture** — System design, tech stack, data model
4. **Planning** — Epic/story breakdown, implementation plan
5. **Development** — Stepwise build (structure > styling > interactions > logic)
6. **Enhancement** — Iterative improvements

---

## Typical Engagement Shape

| Attribute | Value |
|-----------|-------|
| **Duration** | Variable — sprint-based, can be 4 weeks to 12 months |
| **Deliverables** | Working software, deployed and documented |
| **Client time commitment** | 2-4 hours/week (reviews, feedback) |
| **Pricing model** | Hourly, fixed-price per epic, or retainer |
| **Team involved** | PM, Architect, Lead Dev, Dev(s), QA Tester |

---

## Required COS Fields

```yaml
project:
  name, description, tech_stack
  frontend_folder, backend_folder, ports
  package_manager

vibe_os_config:
  markdown_exploder: true/false
  slash_prefix: "/"
  workflow_approach: stepwise

documentation:
  prd_path, architecture_path, qa_path
  sharded: true/false

agents_config:
  orchestrator, dev, lead_dev, architect, qa_tester
  [each with model assignment]

developer_config:
  always_load_files: [list]
  debug_log_path
  story_location

tech_stack:
  frontend: [list]
  auth, database, billing, monitoring

phase:
  current: discovery | requirements | architecture | planning | development | enhancement
```

---

## What a "Correct" Plan Looks Like

1. **PRD exists and is approved** — no code before PRD
2. **Architecture is documented** — stack, data model, component hierarchy
3. **Stories are broken down to 2-8 hour granularity** — nothing larger than 16h un-broken
4. **Stepwise development enforced** — structure > styling > interactions > logic
5. **Testing strategy defined** — what gets tested, at what level
6. **Deployment plan exists** — how it ships, where it lives, who maintains it

---

## Scoping Questions

1. What are you building and why? What problem does it solve?
2. Who's the user? What's their workflow?
3. What's the MVP — the minimum thing that proves value?
4. What tech stack preferences or constraints exist?
5. Who owns hosting and infrastructure?
6. What integrations are required?
7. What's the timeline and budget?
8. Who will maintain this after launch?
9. What's the data model look like?
10. Any compliance or security requirements?

---

## Blocking Gates

1. **Requirements Defined** — PRD complete and approved
2. **Architecture Approved** — system design, tech stack, data model
3. **Stories Ready** — epics broken down, acceptance criteria defined, estimates attached
4. **QA Passed** — code reviewed, tests passing, security scan, requirements traced

---

## Common Pitfalls

- Starting code before PRD is finalised
- Vague acceptance criteria leading to rework
- Not enforcing stepwise development (jumping to logic before styling is done)
- Scope creep without formal change requests
- Skipping QA to hit deadline

---

## When This is the Right Project Type

- Client needs software built (not a playbook, not a framework)
- Requirements are clear enough to write a PRD
- Budget supports dev time
- Tech stack is one Njin can work with (preferred: Next.js, React, Supabase, Clerk, Stripe)

## When It's NOT the Right Project Type

- Client needs a marketing website (AetherFlow)
- Client needs a sales playbook (Njin Method)
- Requirements are vague — do discovery first
- Client expects "AI magic" without a clear use case

---

**Source:** `docs/background/frameworks/vibe-os/`, `docs/background/project-examples/` (vibe project examples).
