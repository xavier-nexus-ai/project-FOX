# Checklist: Scope Gate

**Purpose:** Validate that a scope document meets Njin PM Framework standards before it advances to planning. Run this as the compliance check at the end of the scoping workflow.

**Run by:** Orchestrator (via compliance-check skill), PM (final review)

**Gate:** `scope_approved` in `cos.yaml`

---

## Section 1: Framework Alignment

- [ ] Delivery framework identified and correct for engagement type
- [ ] Framework reference doc in `methodology/frameworks/` was consulted
- [ ] Phase model matches the framework's phase model
- [ ] Every phase has defined deliverables
- [ ] Framework-specific blocking gates are referenced

**Critical rule:** The scope must align to the framework, not the proposal. If the proposal conflicts with the framework, the framework wins.

---

## Section 2: Earliest Possible Win (Mandatory)

- [ ] Earliest Possible Win is identified and specific (not generic)
- [ ] EPW is achievable within the first sprint or first week of delivery
- [ ] EPW is something the client can see, use, or show to someone

**Rule:** A scope without an EPW cannot pass this gate. Full stop.

---

## Section 3: Deliverables Quality

- [ ] Each deliverable is framed as an outcome, not a feature
  - ✅ Good: "Eliminate 10 hours of manual data entry per week"
  - ❌ Bad: "Setup CRM automation"
- [ ] Each deliverable is specific enough to scope and estimate
- [ ] Deliverables are grouped by framework phase
- [ ] Dependencies between deliverables are identified

---

## Section 4: Gaps and Assumptions

- [ ] Any gaps from discovery are explicitly listed
- [ ] Each gap is flagged as hard blocker or nice-to-have
- [ ] Hard blockers have owners and deadlines
- [ ] Nice-to-haves are documented as caveats with impact
- [ ] Assumptions made in scoping are explicit
- [ ] Risks are identified with likelihood and impact

---

## Section 5: Framework-Proposal Alignment

- [ ] Where the proposal and framework align, scope reflects both
- [ ] Where they differ, the conflict is explicitly flagged
- [ ] PM has decided how to resolve any conflicts
- [ ] Client expectations from sales are captured

**If a conflict exists that the PM cannot resolve, escalate to James before proceeding.**

---

## Section 6: Writing Standards

- [ ] Australian English throughout
- [ ] No em dashes (—) anywhere
- [ ] No corporate jargon (leverage, synergy, holistic, robust, comprehensive, multifaceted, paradigm shift)
- [ ] Tables and bullet points used where appropriate (not walls of text)
- [ ] Third-grade reading level for any client-facing content
- [ ] No AI-generated fluff (if it sounds like an AI wrote it, rewrite it)

---

## Section 7: COS Integration

- [ ] Scope document path is recorded in `cos.yaml.deliverables.scope_document`
- [ ] `phase.scoping.deliverables.*` flags updated
- [ ] Change log entry added
- [ ] Gate status is updatable to `passed: true` after PM approval

---

## Section 8: Client Review Readiness (if applicable)

For engagements where the client reviews the scope directly:

- [ ] Communication Agent has a client-facing version ready
- [ ] Voice-scoring passed against client's tone of voice guide (if exists)
- [ ] Technical jargon is translated or removed
- [ ] Outcomes are quantified where possible

---

## Verdict

- **Pass** — All sections checked, scope is ready for PM approval and planning
- **Pass with concerns** — Minor issues that can be noted and addressed in planning
- **Fail** — One or more critical issues; route back to Business Analyst

### Common Fail Reasons

| Fail Reason | Fix |
|-------------|-----|
| Scope built from proposal alone | Route back to BA, require framework consultation |
| No Earliest Possible Win | BA must add before gate can pass |
| Generic deliverables | BA must rewrite as outcomes |
| Corporate jargon present | Orchestrator can rewrite directly; remove jargon |
| Framework conflict unresolved | Escalate to James |
| No gap documentation | BA must complete gap analysis |

---

## Post-Gate Actions (If Pass)

1. Orchestrator updates `cos.yaml`:
   - `gates.scope_approved.passed`: true
   - `gates.scope_approved.checked`: <timestamp>
   - `phase.scoping.status`: complete
2. Change log entry added
3. Handoff prepared for Coordinator (planning phase)
4. GitHub commit

---

*Reference: `methodology/frameworks/pm-discovery-to-delivery.md` Phase 3 (Scoping), `methodology/ways-of-working/writing-standards.md`.*
