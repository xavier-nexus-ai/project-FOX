# Vocabulary Glossary: Njin Method & AI Orchestration

This glossary covers all Njin-specific terms a new project manager needs to understand. Terms are grouped by where you encounter them, not alphabetically.

---

## Core Methodology

**TORQUE**
Njin's 6-phase client journey framework: **T**ransform > **O**bserve > **R**oadmap > **Q**ualify > **U**pgrade > **E**volve. Every Njin Method engagement follows this sequence. The phases describe both the client's progression and the work Njin does at each stage. When someone says "a client is in Roadmap," they mean that phase of TORQUE.

---

**Playbook**
A revenue-focused implementation plan for a specific part of the client's sales and marketing operation. Playbooks target one of four revenue pillars: Acquisition, Conversion, Monetisation, or Retention. A playbook is not a strategy document — it's an operational manual with scripts, automation specs, CRM setup instructions, and rep handbooks. Njin typically delivers two playbooks per Njin Method engagement.

**Context:** You encounter the word "playbook" in almost every client conversation. It is the primary deliverable of the Njin Method, not the framework itself.

---

**The 12 Core Numbers**
The baseline metrics collected from every Njin Method client before any work begins. They tell Njin which revenue pillar is leaking and form the "before" snapshot for measuring impact.

| # | Metric | Category |
|---|--------|----------|
| 1 | Revenue (last 12 months) | Revenue & Growth |
| 2 | Revenue (prior 12 months) | Revenue & Growth |
| 3 | Leads per month | Acquisition |
| 4 | Cost per lead ($) | Acquisition |
| 5 | Lead > Appointment rate (%) | Conversion |
| 6 | Show rate (%) | Conversion |
| 7 | Close rate (%) | Conversion |
| 8 | Average deal size ($) | Conversion |
| 9 | MRR or contract length (months) | Monetisation & Retention |
| 10 | Churn rate (%) or customer lifespan (months) | Monetisation & Retention |
| 11 | Customer LTV ($) | Monetisation & Retention |
| 12 | CAC ($) | Monetisation & Retention |

**Context:** The Core 12 gate everything downstream. You cannot generate system instructions for an LLM project, write a playbook, or run a constraint diagnosis without them logged in the COS.

---

**Constraint Diagnosis**
The analysis run on the Core 12 to identify which revenue pillar is the client's primary bottleneck. The four constraint types are:

- **Acquisition** — Not enough leads coming in
- **Conversion** — Leads exist but aren't becoming clients
- **Monetisation** — Clients buy once but don't spend enough
- **Retention** — Clients churn before they've delivered enough LTV

The output is: Primary constraint, Secondary constraint (what becomes the next bottleneck once the first is fixed), rationale, and 90-day priority.

**Context:** The constraint diagnosis directly determines which playbook type to build and which sections to prioritise.

---

## Client State & Operating System

**COS (Client Operating System)**
A YAML state file that tracks every client's progress through the engagement. It holds the current phase, deliverables status, blocking gates, the Core 12, constraint diagnosis, and a change log. The COS is the single source of truth between sessions — if something changes, it goes in the COS. If it's not in the COS, it didn't happen.

**Context:** Every project has one. You read it before every decision and update it after every meaningful change.

---

**Blocking Gates**
Prerequisites that must be met before a client can progress to the next phase. Gates are binary — pass or fail. They exist to prevent building on incomplete foundations. Common gate types:
- **Data Access Gate** — CRM access, Core 12, client documentation all received
- **Phase Exit Gate** — All required deliverables complete before advancing to the next TORQUE phase
- **Tone of Voice Gate** — ToV created and approved before any copy is generated

**Context:** If a gate isn't cleared, the workflow stops. No exceptions.

---

**Handoff Document**
A structured document created at each agent boundary in the PM framework, carrying all context the next agent needs to do its work. The PM reviews every handoff before passing it to the next agent. Handoff documents prevent context loss between sessions and agents.

**Context:** In multi-agent workflows, handoff documents are how work moves between agents. The spawned agent sandbox means agents can't read each other's files — the handoff document IS the transfer mechanism.

---

## Sales & Onboarding

**Reverse Brief**
A document drafted by Njin (not the client) that summarises the client's problem, the cost of that problem, and the proposed solution. It's sent to the client within 24 business hours of the discovery conversation for approval. The format is always: Problem > Cost of Problem.

**Context:** A reverse brief is how Njin confirms shared understanding before scoping. It is also the trigger for moving into project initiation in GHL.

---

**Activation Promise**
A specific, time-bound commitment made to a prospect during the initial sales call. Format: *"Within X days of payment, you'll have Y running and already saving you Z hours."* Certainty beats information — the activation promise creates concrete expectations and removes friction.

**Context:** Used on sales calls and reinforced in the onboarding activation call. It is what the client is buying in their mind.

---

**Ascension / Selling / Reselling Loop**
The three-track upsell strategy deployed at project phase completion and ongoing success reviews:
- **Ascension** — Offer more complex or higher-value solutions (the next level of engagement)
- **Selling** — Highlight ROI so far to justify the next purchase
- **Reselling** — Push continuity (retain them on a managed service or retainer)

**Context:** This loop is triggered at Step 23 (Next Stage Proposal) in the onboarding flow. Every phase completion should have a next-stage proposal attached.

---

**Quick Win**
A tangible, visible early deliverable — typically something the client can show someone within the first week. In AI Orchestration, it's a vibe-coded tool built during Week 4 of Immersion. In the Njin Method, it's the first activation during the Kickoff Call. Quick wins build client confidence and buy commitment to the harder work ahead.

**Context:** A quick win is not the main deliverable. Its job is to create momentum and trust.

---

## Project Management & Framework

**IP Vault**
The structured repository of extracted intellectual property — frameworks, SOPs, judgement calls, vocabulary, and delivery sequences — pulled from a client's existing knowledge during the Mapping phase. The IP vault is the foundation that the AI framework is built on. In the Njin PM context, it's also used internally to capture Njin's own methodology.

**Context:** If the IP vault is shallow, the framework will be generic. The depth of extraction directly determines the quality of what gets built.

---

**Framework Router**
The decision logic for matching an engagement type to the correct deployment framework (Njin Method, AI Orchestration, VIBE OS, AetherFlow, JK Growth, or OpenClaw). Not a formal document — it's a judgement call embedded in the framework's operating principles.

**Context:** Used at the start of any new engagement to determine which framework governs the delivery.

---

**njin-vibe**
The Njin web-based PMO (Project Management Office) platform. Currently in testing by George. It is the platform that project plans, sprints, epics, and user stories live in. The PM framework's Coordinator has a sync skill that pushes state into njin-vibe at agreed checkpoints.

**Context:** The PM framework is the AI companion layer that populates njin-vibe. The framework doesn't replace it — it feeds it.

---

**Plan Mode**
A Claude Code operating mode where the AI proposes a plan and waits for human approval before executing. Plan mode is mandatory in the Njin PM Framework for anything significant. The rule: 90% planning, 10% building. Approve the plan, then let the agent execute.

**Context:** Plan mode is a safety mechanism against irreversible or expensive mistakes. If in doubt, use it.

---

**Discovery Phase vs Scoping Phase**
Two distinct stages within the Business Analyst's work, run in sequence — never combined.

- **Discovery** — BA creates a plan of required documents. PM reviews. BA analyses what's been provided and flags what's missing. Purpose: understand what we know and what we need.
- **Scoping** — Runs only after discovery is complete. Produces the scope document with deliverables, effort, and constraints. Purpose: define what gets built and when.

**Context:** Michael's Avanti mistake was creating a project plan that jumped straight to scoping without running discovery against the framework delivery procedure. Discovery must come first.

---

**Sprint (Njin definition)**
A fortnightly (two-week) delivery cycle. Sprints are scheduled post-kickoff and run as recurring events. Sprint planning assumes 100% availability, then adjusts based on PM input. Sprint reports go into the COS and are communicated to the client via the Communication Agent.

**Context:** Sprints are not flexible on duration — they're always fortnightly. What's flexible is scope and priority within a sprint.

---

**Initialization Agent**
The one-time setup agent that runs at the start of every client project. It ingests the contract scope, meeting transcripts, and client documents to bootstrap the COS and create the project's personalised CLAUDE.md. It runs once per project, at the start. It is not a recurring tool.

**Context:** Think of the Initialization Agent as the project's birth certificate — it creates the state that everything else reads from.

---

**Orchestrator**
In the PM framework, the Orchestrator IS the PM's entry point — it is the central agent through which all other agents are coordinated. It is not a separate supervisory layer. The PM talks to the Orchestrator; the Orchestrator directs agents, reviews handoffs, and maintains project state.

**Context:** Every project interaction begins with the Orchestrator. It owns the COS and the session flow.
