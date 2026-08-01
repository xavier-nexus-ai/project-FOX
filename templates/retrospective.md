# Retrospective — {{CLIENT_NAME}} {{SPRINT_OR_PHASE_LABEL}}

<!-- Template version: 1.0.0 | Produced by Coordinator agent using the retrospective skill. -->
<!-- Run at end of every sprint and every phase. Data-driven — no guesswork. -->
<!-- ONE recommendation only. If you have more than one, pick the most important. -->

---

## Document Metadata

| Field | Value |
|-------|-------|
| **Client** | {{CLIENT_NAME}} |
| **Sprint / Phase** | {{SPRINT_NUMBER_OR_PHASE_NAME}} |
| **Period** | {{START_DATE}} to {{END_DATE}} |
| **Prepared by** | {{AGENT_OR_PM_NAME}} |
| **Date** | {{YYYY-MM-DD}} |
| **Sprint plan ref** | {{SPRINT_PLAN_PATH}} |

---

## 1. Planned vs Actual

<!-- Compare what was committed at sprint start to what was delivered. Be factual. -->

| Story ID | Story title | Committed (hrs) | Actual (hrs) | Status |
|----------|-------------|-----------------|--------------|--------|
| {{CLIENT_PREFIX}}-S{{N}} | {{STORY_TITLE}} | {{HOURS}} | {{HOURS}} | Done / Slipped / Partial |
| {{CLIENT_PREFIX}}-S{{N}} | {{STORY_TITLE}} | {{HOURS}} | {{HOURS}} | Done / Slipped / Partial |

**Sprint goal 1:** {{GOAL}} — {{Achieved / Not achieved}}
**Sprint goal 2:** {{GOAL}} — {{Achieved / Not achieved}}
**Sprint goal 3:** {{GOAL}} — {{Achieved / Not achieved}}

---

## 2. Completion Rate

<!-- Calculate from stories completed vs stories committed. -->

| Metric | Value |
|--------|-------|
| Stories committed | {{NUMBER}} |
| Stories completed | {{NUMBER}} |
| Stories slipped | {{NUMBER}} |
| Completion rate | {{PERCENTAGE}}% |
| Hours committed | {{HOURS}} |
| Hours delivered | {{HOURS}} |
| Hours slipped | {{HOURS}} |

---

## 3. Velocity

<!-- Track points or hours delivered per sprint. Compare to previous sprints if available. -->

| Sprint | Hours delivered | Completion rate |
|--------|-----------------|-----------------|
| Sprint {{N-2}} | {{HOURS}} | {{%}} |
| Sprint {{N-1}} | {{HOURS}} | {{%}} |
| Sprint {{N}} (this sprint) | {{HOURS}} | {{%}} |

**Trend:** {{Improving / Stable / Declining}}

> If first sprint, leave prior sprint rows blank.

---

## 4. Slipped Items

<!-- List every story or goal that did not complete. State why. -->
<!-- Do not leave this section vague — "ran out of time" is not an explanation. -->

| Story ID | Story title | Reason for slipping | Action |
|----------|-------------|---------------------|--------|
| {{CLIENT_PREFIX}}-S{{N}} | {{STORY_TITLE}} | {{SPECIFIC_REASON}} | Move to Sprint {{N+1}} / Descope / Blocked — chase {{OWNER}} |

> If nothing slipped, write "All committed stories completed."

---

## 5. Wins

<!-- 3 maximum. What went well? Be specific — "good communication" is not a win. -->
<!-- "Client approved ToV guide within 24 hours, removing the blocking gate" is a win. -->

1. {{WIN_1}}
2. {{WIN_2}}
3. {{WIN_3}}

---

## 6. Concerns

<!-- 3 maximum. What is causing friction? Be specific and name the root cause. -->
<!-- "Estimates were off" is not a concern. "Discovery interviews took 6 hours vs 2 estimated because client had no documented processes" is. -->

1. {{CONCERN_1}}
2. {{CONCERN_2}}
3. {{CONCERN_3}}

---

## 7. Patterns

<!-- What patterns are emerging across sprints? -->
<!-- Only populate from Sprint 2 onwards. Leave blank for Sprint 1. -->
<!-- Patterns are observations, not recommendations — save the recommendation for Section 8. -->

{{PATTERNS_OBSERVED}}

> Examples: "External dependencies are consistently the primary cause of slippage." / "Estimates are running 30% low on discovery-type tasks." / "Client approval turnaround is faster than expected."

---

## 8. Recommendation

<!-- ONE recommendation. The most important thing to change in the next sprint. -->
<!-- If you have more than one, pick the one with the highest impact and log the rest as backlog. -->

**Recommendation:** {{ONE_SPECIFIC_RECOMMENDATION}}

**Why this one:** {{ONE_SENTENCE_RATIONALE}}

**Owner:** {{WHO_IMPLEMENTS_IT}}

**By:** Next sprint kickoff / {{DATE}}

---

*Retrospective — Njin PM Framework v1.0. Produced by Coordinator agent using retrospective skill.*
