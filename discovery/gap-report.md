# Discovery Gap Report
**Client:** Fox Finance Group Pty Ltd
**Date:** 2026-05-01
**Produced by:** Insight (Business Analyst)
**Status:** Updated — verbatim transcript added 2026-05-01

---

## Document Analysis Notes

### Transcript — Apr 20 2026 (AI Summary) — SUPERSEDED
Replaced by verbatim transcript. See below.

---

### Transcript — Apr 20 2026 (Verbatim) — PROVIDED (full quality)

**Covers:** Full 42-minute conversation between James Killick, Rowdie Lang, and Xavier Ybanez. All topics confirmed: marketing system, lead magnets, EV loan opportunity, cross-sell pipeline architecture, nurture sequences, customer routing logic, data integration (Ambition → SendGrid → GHL), reactivation campaign, GHL/Twilio setup, project scope meeting scheduling.

**Additional detail not in AI summary:**
- **ICA data already sent to James** — Rowdie said "the ICA data I sent across" at @31:44. Some ICA documentation exists with James but is not in `Docs/background/`.
- **3CX** — Rowdie is running a phone system called 3CX. Mentioned at @19:37 ("I'll just turn 3CX off"). This is part of the current comms stack.
- **LMG (Loan Market Group)** — A second aggregator Rowdie is evaluating as a potential Ambition replacement. Their API capability is being assessed. This may affect the data integration scope.
- **Maddie** — James mentioned "just you, Nathan and Maddie that has access" when discussing restricted GHL data access. Maddie's role is unknown — needs clarification.
- **Fox Home Loans is a separate entity** — The cross-sell pipeline spans two distinct business units: Fox Finance Group (FFG — asset finance) and Fox Home Loans (FHL — home loans). These have separate teams and different nurture cadences (FFG: 6-12 months; FHL: 18 months).
- **Engagement pricing** — James offered a $27k-value framework workshop for free given Rowdie's technical capability. Suggests this engagement may be discounted or pro bono. Needs commercial confirmation.
- **Xavier confirmed present** — Xavier was in the meeting and confirmed as working on project scope with George.

**Still does not cover:** Commercial terms or contract value, Thursday scope meeting outcomes, Nathan Drew's direct input.

---

### Operational Master Document — PARTIAL QUALITY

**Covers:** Four loan pillars with sub-types and value propositions, initial assessment framework (qualifying questions for GHL forms), 5-step operational SOP (Apply > Documents > Approved > Sign > Settle), company credentials.

**Does not cover:** Team structure, business health data (revenue, lead volume, conversion rates), existing GHL configuration, current lead sources, how follow-up/nurture currently works in practice, ICA definitions, existing automation, integration landscape beyond Ambition and GHL.

**Key gap:** Written as a reference document, not a workflow specification. Describes what the business does, not how GHL is currently configured or what needs to be built.

---

## Hard Blockers

These must be resolved before scoping can begin.

### B1 — Signed Contract
**Why it blocks:** Scoping gate is binary — cannot pass without a signed contract.

**Request to James / George:**
> Can you confirm the contract status with Nathan and Rowdie? We need a signed copy in `Docs/background/` before the scope document can be written. If the contract hasn't been sent yet, that needs to happen this week.

---

### B2 — Framework Type Confirmation
**Why it blocks:** If this is a Playbook + VIBE OS engagement rather than AI Orchestration, the delivery sequence, deliverables, and scope document all change. Scoping against the wrong framework produces a useless scope document.

**Request to James / George:**
> The Apr 20 transcript describes a GHL CRM build and playbook creation — not an AI Orchestration IP extraction engagement. Can you confirm: is this a Playbook build, a VIBE OS build, or a combination of both? This determines the entire scope structure and delivery sequence.

---

### B3 — Timeline Confirmation
**Why it blocks:** The project COS records 5 weeks (target completion 2026-06-05). The timeline PDF shows a 10-week project. Scoping against the wrong timeline produces the wrong plan.

**Request to James / George:**
> The COS has a target completion of 2026-06-05 (5 weeks from start). The timeline document shows 10 weeks. Which is correct? Once confirmed, the COS will be updated and the scope document will be built against the right timeline.

---

### B4 — GHL Access Confirmation
**Why it blocks:** No GHL build work can be scoped or started without confirmed access to the live Fox Finance GHL account.

**Request to Rowdie Lang:**
> Can you confirm that the Njin team (James / Xavier) has been granted access to the Fox Finance GHL account? If not yet done, please provide the subscription link James mentioned in the Apr 20 call, or grant team access directly from within GHL settings.

---

## Significant Gaps

These are needed before the scope document can be written.

### S1 — Scope of Work / Proposal PDF
**Why it matters:** Without knowing what was sold, we can't verify the scope document matches the commercial agreement.

**Request to George / James:**
> Please provide the proposal or scope of work that was shared with Nathan and Rowdie. A PDF or link is fine. Drop it into `Docs/background/`.

---

### S2 — ICA / Customer Profile Documentation
**Why it matters:** Nurture sequences, GHL pipeline stages, and routing logic all depend on defined ICAs. Without this, the CRM build cannot be scoped correctly.

**Update from verbatim transcript:** Rowdie mentioned at @31:44 "the ICA data I sent across" — some ICA documentation was already sent to James. This is PARTIALLY RESOLVED but the document is not in `Docs/background/`.

**Request to James:**
> Rowdie mentioned sending you ICA data in or before the Apr 20 call. Can you share that document or add it to `Docs/background/`? This will reduce the burden on Rowdie to redo work already done.

**Request to Rowdie Lang (if above is incomplete):**
> We need: (1) your main customer profiles by loan type, and (2) the key data points that route a customer to the correct nurture sequence — particularly the if-then logic James described (e.g. "if asset-backed AND no mention of new purchase → refinance pathway"). The routing matrix needs to cover both Fox Finance Group and Fox Home Loans sequences.

---

### S3 — Current GHL Pipeline Documentation
**Why it matters:** We need to know what's already in GHL before scoping what needs to be built — building on top of existing config vs. starting from scratch are very different scopes.

**Request to Rowdie Lang:**
> Can you export or screenshot the current GHL pipeline view — specifically the pipeline stages, any existing automations, and the contact record fields you currently use? Even a screen recording walking through the current setup would work.

---

### S4 — Customer Data Field Map (Ambition → GHL)
**Why it matters:** The data integration scope depends entirely on which fields need to move from Ambition to GHL and how they map.

**Request to Rowdie Lang:**
> From the Apr 20 call, you were going to review the Ambition data and flag fields as critical / key / nice-to-have for GHL import. When that's ready, send it through. A simple table with field name and priority level is all we need.

---

## Nice to Have

| # | Item | Status | Request |
|---|---|---|---|
| N1 | Verbatim transcript — Apr 20 2026 | PROVIDED — added to `Docs/background/` 2026-05-01 | Done. |
| N2 | Existing nurture sequences / email templates | MISSING | Rowdie: do you have any existing email sequences or templates in GHL or elsewhere? Share if available. |
| N3 | Ambition CRM export sample | MISSING | A sample CSV export (anonymised is fine) would help map data fields for integration scoping. |
| N4 | Reverse Brief | MISSING | A few dot points from Rowdie / Nathan on what they expect the engagement to deliver — email is fine. |
| N5 | Maddie — role clarification | MISSING | James mentioned "just you, Nathan and Maddie" having GHL access. Who is Maddie and what is her role? |
| N6 | LMG API assessment outcome | PENDING | Rowdie is awaiting LMG's response on API capability. If LMG replaces Ambition as the data source, integration scope changes. Flag when confirmed. |

---

## Documents Added Post-Discovery (2026-05-04)

The following docs were added to `Docs/background/` after the initial discovery pass. None resolve B1–B4.

| Document | Impact on Scope |
|---|---|
| Fox Tone of Voice.docx | Was present in initial commit — not previously reviewed. Informs nurture sequence copy and email tone. |
| FFG Writing Guidelines Content Tone Of Voice.docx | Detailed ToV + StoryBrand framework. Informs all content automation scope — sequences, lead magnets, CTA copy. |
| Brand Promise & Company Values.docx | Brand promise + 6 values. Use in onboarding communications and nurture sequence framing. |
| Fox Finance Group Branding Guide.pdf | Logo, colours, fonts. Required before building any GHL branded templates or designed deliverables. |
| FFG Site Map.docx | Full FFG URL map. Enables accurate CTA routing in automation sequences; scopes lead magnet landing page integration. |
| FHL Site Map.docx | Full FHL URL map. Enables cross-sell pipeline scoping; home loan nurture CTA routing. |

**Hard blockers B1–B4 remain open.** These docs do not substitute for contract, framework confirmation, timeline confirmation, or GHL access.

---

## Workflow Decision

Four hard blockers exist (B1–B4). Per framework rules, this triggers a pause-and-notify workflow. However, the PM has instructed discovery to proceed with available materials.

**Agreed path:**
- PM to chase B2 + B3 (framework type + timeline) with James / George — internal, resolvable quickly
- PM to chase B4 (GHL access) with Rowdie — simple confirmation
- B1 (contract) is a formal scoping gate blocker — discovery report will be produced but scoping gate is held until contract is signed
- S1–S4 to be collected before scope document is written
- N1 (verbatim transcript) — DONE, added to `Docs/background/` and committed to Xavier branch 2026-05-01

---

*Produced by Insight (Business Analyst) — Njin PM Framework — 2026-05-01*
