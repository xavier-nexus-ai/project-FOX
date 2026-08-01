# Project Plan — {{CLIENT_NAME}}

<!-- Template version: 1.0.0 | Populate all {{PLACEHOLDERS}} before submitting for PM review. -->
<!-- This document is produced by the Coordinator agent and reviewed by the PM. -->
<!-- Gate: plan_ready must pass before sprint execution begins. -->
<!-- Every deliverable from the scope document must appear here. QA Tester will trace it. -->

---

## Document Metadata

| Field | Value |
|-------|-------|
| **Client** | {{CLIENT_NAME}} |
| **Engagement type** | {{ENGAGEMENT_TYPE}} |
| **Framework** | {{DELIVERY_FRAMEWORK}} |
| **Prepared by** | {{AGENT_OR_PM_NAME}} |
| **Date** | {{YYYY-MM-DD}} |
| **Version** | {{VERSION_NUMBER}} |
| **Scope document ref** | {{SCOPE_DOCUMENT_PATH}} |
| **Status** | Draft / PM Reviewed / Approved |

---

## 1. Overview

<!-- 2-3 sentences. What does this plan cover, how many sprints, and what's the overall arc? -->

{{PLAN_OVERVIEW}}

**Total sprints:** {{TOTAL_SPRINTS}}
**Sprint cadence:** {{SPRINT_LENGTH}} (e.g. 2 weeks)
**Planned start:** {{START_DATE}}
**Planned end:** {{END_DATE}}

---

## 2. Phases and Epics

<!-- One section per phase. Within each phase, list the epics. -->
<!-- Every epic must trace back to a deliverable in the scope document. -->

### Phase {{PHASE_NUMBER}}: {{PHASE_NAME}}

> {{PHASE_DESCRIPTION}} — what is this phase delivering and what gate closes it?

| Epic ID | Epic name | Scope deliverable ref | Sprint(s) |
|---------|-----------|-----------------------|-----------|
| {{CLIENT_PREFIX}}-E{{N}} | {{EPIC_NAME}} | {{SCOPE_DELIVERABLE_REF}} | {{SPRINT_NUMBERS}} |

### Phase {{PHASE_NUMBER}}: {{PHASE_NAME}}

| Epic ID | Epic name | Scope deliverable ref | Sprint(s) |
|---------|-----------|-----------------------|-----------|
| {{CLIENT_PREFIX}}-E{{N}} | {{EPIC_NAME}} | {{SCOPE_DELIVERABLE_REF}} | {{SPRINT_NUMBERS}} |

> Add phase sections as needed.

---

## 3. Epics with Stories

<!-- For each epic, list the stories that make it up. -->
<!-- Stories must be in "As a X, I want Y, so that Z" format. -->
<!-- See individual story files in docs/stories/ for full acceptance criteria. -->

### {{CLIENT_PREFIX}}-E{{N}}: {{EPIC_NAME}}

| Story ID | Story title | Estimate (hrs) | Sprint |
|----------|-------------|----------------|--------|
| {{CLIENT_PREFIX}}-S{{N}} | {{STORY_TITLE}} | {{HOURS}} | {{SPRINT_NUMBER}} |
| {{CLIENT_PREFIX}}-S{{N}} | {{STORY_TITLE}} | {{HOURS}} | {{SPRINT_NUMBER}} |

**Epic total estimate:** {{TOTAL_HOURS}} hrs

> Repeat for each epic.

---

## 4. Timeline

<!-- Visual summary of phases and key milestones. Use a table. -->

| Sprint | Dates | Phase | Key deliverables | Gate |
|--------|-------|-------|-----------------|------|
| Sprint 1 | {{START}} to {{END}} | {{PHASE}} | {{DELIVERABLES}} | {{GATE}} |
| Sprint 2 | {{START}} to {{END}} | {{PHASE}} | {{DELIVERABLES}} | {{GATE}} |
| Sprint 3 | {{START}} to {{END}} | {{PHASE}} | {{DELIVERABLES}} | {{GATE}} |

> Add rows as needed.

---

## 5. Capacity

<!-- How much capacity is available per sprint? -->
<!-- Estimate must be realistic — not theoretical maximum. -->

| Resource | Role | Hours/sprint | Notes |
|----------|------|--------------|-------|
| {{PM_NAME}} | PM | {{HOURS}} | {{NOTES}} |
| {{RESOURCE_NAME}} | {{ROLE}} | {{HOURS}} | {{NOTES}} |
| {{CLIENT_NAME}} | Client stakeholder | {{HOURS}} | For reviews, approvals, access |

**Total capacity per sprint:** {{TOTAL_HOURS_PER_SPRINT}} hrs

**Buffer (20%):** {{BUFFER_HOURS}} hrs

**Available for delivery per sprint:** {{DELIVERY_HOURS}} hrs

---

## 6. Dependencies

<!-- List every dependency that could block delivery. External = outside the PM's control. -->

| Dependency | Type | Blocks | Owner | Due |
|------------|------|--------|-------|-----|
| {{DEPENDENCY}} | Internal / External | {{WHAT_IT_BLOCKS}} | {{OWNER}} | {{DATE}} |

---

## 7. Risks

<!-- Risks specific to this plan. Cross-reference scope document risks where relevant. -->

| Risk | Likelihood | Impact | Mitigation | Owner |
|------|------------|--------|------------|-------|
| {{RISK}} | H/M/L | H/M/L | {{MITIGATION}} | {{OWNER}} |

---

## 8. Sprint Breakdown

<!-- Summary of what is committed to each sprint. Full sprint plans are in docs/sprints/. -->

| Sprint | Goals | Stories | Estimate | Capacity |
|--------|-------|---------|----------|----------|
| Sprint 1 | {{GOALS}} | {{STORY_IDS}} | {{HOURS}} | {{CAPACITY}} |
| Sprint 2 | {{GOALS}} | {{STORY_IDS}} | {{HOURS}} | {{CAPACITY}} |
| Sprint 3 | {{GOALS}} | {{STORY_IDS}} | {{HOURS}} | {{CAPACITY}} |

---

## Approvals

| Role | Name | Date | Status |
|------|------|------|--------|
| PM | {{PM_NAME}} | {{DATE}} | Pending / Approved |
| QA Tester | Verify | {{DATE}} | Not reviewed / Pass / Concerns / Fail |

---

*Project Plan — Njin PM Framework v1.0. Produced by Coordinator agent.*
