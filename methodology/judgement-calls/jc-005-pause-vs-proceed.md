# Judgement Call 5: When to Pause a Workflow vs Proceed with Caveats

**Title:** Workflow Gate Decision — Hard Stop vs Caveat and Continue

**The Decision:** When the Business Analyst flags missing documents or incomplete information, does the workflow pause entirely or proceed with documented caveats?

**Two-path decision:**

| Situation | Decision |
|-----------|----------|
| Missing info is a **critical blocker** (contract scope, CRM access, Core 12, client approval) | Hard stop. Log in COS. Escalate. Do not proceed. |
| Missing info is a **nice-to-have** (brand guidelines, old scripts, competitor research, call recordings) | Proceed with caveat. Document the gap. Chase in parallel. |

**Critical blockers — workflow pauses:**
- Contract scope not confirmed (no foundation for the project plan)
- CRM access not granted (can't build pipelines or automations)
- Core 12 not collected (can't diagnose constraint or personalise playbook)
- Tone of Voice not created or approved (can't generate copy that sounds like the client)
- Phase exit gate not met (blocking gates exist precisely for this — do not bypass them)

**Nice-to-haves — workflow continues with caveats:**
- Brand guidelines missing > use inferred tone, flag as unvalidated
- Old scripts missing > draft from scratch, flag as new baseline
- Case studies missing > add placeholders marked [ADD TESTIMONIAL]
- Interview not yet scheduled > proceed, add to follow-up queue

**How to document a caveat:**
- Add a note to the relevant COS field (data_access or notes)
- Flag it in the handoff document so the next agent knows
- Do not silently skip it — hidden gaps create problems downstream

**Default:** When in doubt about whether something is a hard blocker, treat it as one. It's faster to pause and confirm than to build on a wrong foundation and rework it later.

**Source:** Apr 7 meeting transcript (open question on BA gap handling), Playbook Creation SOP Step 5 (Prerequisite Validation), AI Transformation SOP (blocking gate enforcement).
