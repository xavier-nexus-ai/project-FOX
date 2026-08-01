# Scoping Guide: AI Orchestration Client (90-Day Build)

Use this guide when running discovery and scoping for an AI Orchestration engagement.

---

## Required Documents (Before Scoping Starts)

- [ ] Signed contract
- [ ] Sales handover bundle
- [ ] Sales and discovery call transcripts
- [ ] Client's existing IP materials (any format)

---

## Business Context

- [ ] **Client name / company** — ___
- [ ] **Industry** — ___
- [ ] **Business model** — coaching / consulting / agency / course-creator / SaaS / professional services / hybrid
- [ ] **Annual revenue** — $___ (or "confidential")
- [ ] **Team size and composition** — ___
- [ ] **Primary offer** — ___
- [ ] **Pricing model** — ___
- [ ] **Delivery model** — 1:1 / group / self-paced / hybrid
- [ ] **Target audience (ICP)** — ___
- [ ] **Locale / timezone** — ___

---

## Business Health Numbers

Collect what's available — don't block on missing values:

- [ ] **Annual revenue** — $___
- [ ] **Revenue model** — (retainer / project / hybrid / subscription)
- [ ] **Active clients** — ___
- [ ] **Hours per client (average)** — ___
- [ ] **Founder delivery hours per week** — ___
- [ ] **Revenue per founder hour** — $___
- [ ] **Max capacity** — ___ clients
- [ ] **Leads per month** — ___
- [ ] **Lead-to-client conversion rate** — ___%
- [ ] **Average engagement value** — $___
- [ ] **Client lifetime value** — $___

---

## IP Audit (Critical — This Determines Feasibility)

The AI Orchestration build extracts the client's existing IP. If they don't have any, the build can't produce a meaningful framework. Ask:

- [ ] **Frameworks** — Do you have named, structured approaches to solving problems for your clients? List them.
- [ ] **Methodologies** — Do you have a named methodology? What's it called? What are the phases?
- [ ] **SOPs** — Do you have step-by-step processes for how you deliver? Where are they documented?
- [ ] **Playbooks** — Do you have operational guides for specific functions?
- [ ] **Templates** — Do you have document templates you reuse (proposals, reports, etc.)?
- [ ] **Scripts** — Do you have sales scripts, onboarding scripts, client conversation guides?
- [ ] **Case studies** — Do you have documented client success stories?

**Decision point:** If the client has no structured IP, escalate to James. AI Orchestration may not be the right framework — consider Njin Method first to generate IP.

---

## Source Materials Catalog

Every existing document the client provides goes into the catalog:

```yaml
source_materials:
  - name: [document name]
    type: [framework | sop | course_content | transcript | template | brief | other]
    path: [file path]
    format: [pdf | docx | markdown | video | audio | other]
    processed: false
```

**Required from client:**
- [ ] All courses and course outlines
- [ ] All existing frameworks and methodologies
- [ ] All SOPs and processes
- [ ] Templates and deliverable examples
- [ ] Case studies and testimonials
- [ ] Sales and delivery call recordings (transcripts preferred)
- [ ] Brand voice / tone of voice documentation

---

## Delivery Process Mapping

Understand how the client currently delivers:

- [ ] **Walk me through a typical client journey** — from first contact to completion
- [ ] **Where do you use templates vs bespoke work?**
- [ ] **Where do you (the expert) have to touch the work personally?**
- [ ] **What parts of delivery are already systematised?**
- [ ] **Where do things break or slow down?**
- [ ] **What takes the most time that isn't high-value?**

---

## Tone of Voice Materials

Required for the Tone of Voice Gate during Immersion:
- [ ] Website copy
- [ ] Email sequences / newsletters
- [ ] Sales call recordings or transcripts
- [ ] Social media posts
- [ ] Podcast or video content (if applicable)
- [ ] Client-facing documents (proposals, reports)

---

## Technical Prerequisites

- [ ] **Claude Code installed** on client's machine (or willing to install in Week 1)
- [ ] **API key** available
- [ ] **Dedicated project folder** on client's machine
- [ ] **Git familiarity** — basic understanding (will be taught if needed)
- [ ] **Internet and stable work environment** for synchronous sessions

---

## Time Commitment Verification

The engagement requires **4-6 hours/week from the client for 12 weeks**, with peaks in Weeks 5-6 (6+ hours for IP extraction interviews).

- [ ] **Can the client commit this time?** Confirm explicitly.
- [ ] **What weeks are they unavailable?** (Leave, travel, other commitments)
- [ ] **Who is the decision-maker for methodology naming and major decisions?** (Should be ONE person, not a committee)

---

## Goals & Success Criteria

- [ ] **What does success look like at the end of 90 days?**
- [ ] **What's the 12-month vision for how AI changes their business?**
- [ ] **What's the "Earliest Possible Win" they want to see?**
- [ ] **Will they deploy the framework to their first customer in Week 12?** (Required for the build to be validated)

---

## Pre-Immersion Prerequisites

Before Week 1 starts:
- [ ] Project folder created on client's machine
- [ ] All source materials transferred to project folder
- [ ] Builder framework deployed (`scripts/aob deploy /path/to/project`)
- [ ] COS initialised
- [ ] Kick-off meeting scheduled
- [ ] First session booked (AI Literacy Week 1)

---

## Discovery Gaps Template

```markdown
## Gaps Identified

### Hard Blockers (cannot proceed without)
- Client has no existing IP — framework build not feasible (escalate to James)
- Claude Code cannot be installed — delivery constraint
- Client cannot commit weekly time — engagement will fail

### Nice-to-Haves (proceed with caveat)
- Case studies not yet collected — gather in Week 5 during IP extraction
- Specific SOP docs missing — extract from interview instead
```

---

## Minimum IP Extraction Targets

These are the gate requirements for the end of Mapping:

- [ ] **2+ frameworks** extracted
- [ ] **3+ SOPs** extracted
- [ ] **5+ judgement calls** extracted
- [ ] **Vocabulary** captured in client's own language
- [ ] **Delivery sequences** mapped

If the client has less than this available, the engagement is at risk. Flag it early.

---

**Source:** `docs/background/sop-ai-transformation.md`, `docs/background/frameworks/ai-orchestration/`, `docs/ip-vault/delivery-sequences/ds-003-ai-transformation-delivery.md`.
