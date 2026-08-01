# Compliance Report — {{CLIENT_NAME}}

<!-- Template version: 1.0.0 | Produced by QA Tester agent (Verify) or Tone of Voice Agent (Resonance). -->
<!-- The overall verdict must appear in the first line of the report body. Never bury it. -->
<!-- Gate decision: PASS advances the phase. CONCERNS allows progress with conditions. FAIL halts the phase. -->

---

## Document Metadata

| Field | Value |
|-------|-------|
| **Client** | {{CLIENT_NAME}} |
| **Report date** | {{YYYY-MM-DD}} |
| **Reviewed by** | {{AGENT_NAME}} ({{AGENT_CODENAME}}) |
| **Review type** | Compliance / Voice Scoring |
| **Phase gate** | {{GATE_NAME}} |
| **Status** | Draft / Final |

---

## Verdict

<!-- STATE THE VERDICT FIRST. Do not make the reader hunt for it. -->

> **OVERALL VERDICT: {{PASS / CONCERNS / FAIL}}**

{{ONE_SENTENCE_SUMMARY_OF_VERDICT}}

---

## What Was Reviewed

<!-- List every document or content item reviewed. Include file paths where applicable. -->

| Item | Type | File path / reference |
|------|------|-----------------------|
| {{ITEM_NAME}} | Scope doc / Plan / Story / Content / Guide | {{FILE_PATH_OR_REF}} |

---

## Checks Run

<!-- One row per check. Verdict per check: Pass / Concerns / Fail. -->
<!-- Include a one-line reason for every non-Pass result. -->

| Check | Verdict | Notes |
|-------|---------|-------|
| Framework alignment | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| All required sections present | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| Deliverables as outcomes (not features) | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| Requirements traceability (scope to plan) | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| Story format correct ("As a X...") | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| Acceptance criteria specific and verifiable | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| Estimates attached to all stories | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| Capacity confirmed against committed hours | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| Dependencies identified | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| Earliest Possible Win identified (Sprint 1) | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |
| {{ADDITIONAL_CHECK}} | {{Pass / Concerns / Fail}} | {{REASON_IF_NOT_PASS}} |

> Add or remove rows based on review type. For voice scoring reviews, replace with voice-specific checks.

---

## Issues Found

<!-- List every issue identified. Be specific: quote the exact problem, state the location, explain why it matters. -->
<!-- If verdict is PASS, write "None." -->

### Issue {{N}} — {{SEVERITY: Critical / Major / Minor}}

**Location:** {{FILE_PATH_OR_SECTION}}
**Problem:** {{SPECIFIC_DESCRIPTION_OF_THE_ISSUE}}
**Why it matters:** {{IMPACT_IF_NOT_FIXED}}
**Fix required:** {{WHAT_NEEDS_TO_CHANGE}}

> Add issue sections as needed. Critical issues produce a FAIL verdict. Minor issues may produce CONCERNS.

---

## Recommendations

<!-- What specifically needs to change before this can pass? -->
<!-- Assign each recommendation to an agent or role. -->

| Recommendation | Owner | Priority | Deadline |
|----------------|-------|----------|----------|
| {{RECOMMENDATION}} | {{OWNER}} | Critical / Major / Minor | {{DATE_OR_BEFORE_NEXT_SPRINT}} |

> If PASS, write "No changes required."

---

## Traceability Summary

<!-- For scope and plan reviews only. Delete this section for other review types. -->

| Scope deliverable | Plan entry | Status |
|-------------------|------------|--------|
| {{SCOPE_DELIVERABLE}} | {{PLAN_ENTRY_REF}} | Traced / Gap / Scope creep |

> Gaps = scope items with no plan entry. Scope creep = plan items with no scope entry.

---

## Next Steps

<!-- What happens after this report? Who does what? -->

| Action | Owner | By when |
|--------|-------|---------|
| {{ACTION}} | {{OWNER}} | {{DATE}} |

---

*Compliance Report — Njin PM Framework v1.0. Produced by QA Tester (Verify) or Tone of Voice Agent (Resonance).*
