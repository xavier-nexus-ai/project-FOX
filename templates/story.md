# {{CLIENT_PREFIX}}-S{{STORY_NUMBER}}: {{STORY_TITLE}}

<!-- Template version: 1.0.0 | Populate all {{PLACEHOLDERS}} before sprint commitment. -->
<!-- Stories must have acceptance criteria defined before a sprint starts. -->
<!-- QA Tester reviews story format and criteria specificity as part of plan_ready gate. -->

---

## Story Metadata

| Field | Value |
|-------|-------|
| **Story ID** | {{CLIENT_PREFIX}}-S{{STORY_NUMBER}} |
| **Epic** | {{EPIC_ID}} — {{EPIC_NAME}} |
| **Sprint** | Sprint {{SPRINT_NUMBER}} |
| **Status** | Backlog / Committed / In Progress / Done |
| **Assignee** | {{ASSIGNEE}} |
| **Date created** | {{YYYY-MM-DD}} |
| **Project Dashboard** | {{NOTION_PROJECT_DASHBOARD_URL}} |

---

## User Story

<!-- Format: As a [role], I want [capability], so that [benefit]. -->
<!-- The role must be a real person type — not "the system" or "the user". -->
<!-- The benefit must state the business value, not just describe the capability. -->

**As a** {{ROLE}},
**I want** {{CAPABILITY}},
**so that** {{BUSINESS_BENEFIT}}.

---

## Acceptance Criteria

<!-- 2-4 criteria. Each must be specific and verifiable — binary pass/fail. -->
<!-- "The document is complete" is not verifiable. "All 11 sections of the scope document are populated" is. -->
<!-- Do not write more than 4 criteria — if there are more, split the story. -->

1. {{ACCEPTANCE_CRITERION_1}}
2. {{ACCEPTANCE_CRITERION_2}}
3. {{ACCEPTANCE_CRITERION_3}}

> Add a 4th only if essential. If you have 5+, split the story.

---

## Effort Estimate

| Field | Value |
|-------|-------|
| **Estimate** | {{HOURS}} hrs |
| **Estimation method** | {{T-SHIRT_SIZE_OR_HOURS}} |
| **Confidence** | High / Medium / Low |
| **Notes** | {{ESTIMATION_NOTES_OR_ASSUMPTIONS}} |

> Low confidence estimates should be flagged in the sprint plan as at-risk.

---

## Dependencies

<!-- What must be done before this story can start or complete? -->
<!-- Link to the blocking story or external dependency. -->

| Dependency | Type | Story / task | Status |
|------------|------|--------------|--------|
| {{DEPENDENCY}} | Internal / External | {{REF}} | Outstanding / Resolved |

> If no dependencies, write "None."

---

## Epic Link

**Epic:** {{EPIC_ID}} — {{EPIC_NAME}}

**Scope deliverable ref:** {{SCOPE_DOCUMENT_DELIVERABLE_REF}}

> Every story must trace back to a scoped deliverable. If it doesn't, check whether this is scope creep.

---

*Story — Njin PM Framework v1.0. Produced by Coordinator or Product Owner agent.*
