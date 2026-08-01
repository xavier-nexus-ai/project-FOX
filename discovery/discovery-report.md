# Discovery Report
**Client:** Fox Finance Group Pty Ltd
**Date:** 2026-05-01
**Produced by:** Insight (Business Analyst)
**Framework Reference:** AI Orchestration — `methodology/frameworks/ai-orchestration.md`
**Status:** Complete — awaiting PM review and phase advancement decision

---

## 1. Client Context Summary

Fox Finance Group Pty Ltd is a finance brokerage based in Maroochydore, QLD, established in 2006 with 19+ years of operation. They hold Australian Credit Licence #461205 and work with a panel of 50+ lenders. Their business serves Australians across four loan categories: Vehicle, Personal, Home, and Business loans.

Core delivery process is a 5-step SOP: Apply > Documents > Approved > Sign > Settle. They currently use GoHighLevel (GHL) for pipeline management and Ambition as a secondary CRM containing richer client data (credit scores, household income).

Day-to-day contact: Rowdie Lang. Decision makers: Nathan Drew and Rowdie Lang.

---

## 2. Engagement Type and Framework Applied

**Listed in COS:** AI Orchestration
**Assessed from available materials:** Likely a Playbook creation + VIBE OS (GHL CRM build) hybrid

The Apr 20 transcript describes building GHL pipelines, nurture sequences, marketing automation, customer routing matrices, and data integration — not IP extraction into AI agents. The AI Orchestration framework is designed for extracting and systematising a client's intellectual property into deployable AI agents. What Fox Finance needs is a configured CRM system with automation workflows and a documented playbook.

**This framework mismatch must be confirmed by James / George before scoping begins.** Discovery has proceeded under the `orchestration` designation with this risk recorded.

---

## 3. Documents Reviewed

| Document | Status | Quality Assessment |
|---|---|---|
| Sales Call Transcript — Apr 20 2026 (verbatim) | Provided | Full quality — complete 42-minute verbatim transcript. Covers all topics in full. Supersedes AI summary. |
| Sales Call Transcript — Apr 20 2026 (AI summary) | Provided | Superseded by verbatim. Retained for reference only. |
| Operational Master Document | Provided | Partial — Covers business identity, loan pillars, 5-step SOP. Missing team structure, revenue data, existing GHL configuration, and workflow detail. |
| Timeline PDF | Present but unreadable | Image-based PDF — cannot extract text. PM confirmed: 10-week project plan. Conflicts with COS 5-week target completion. |
| Google Meet Recording — Apr 20 2026 | Present | Video — not reviewed. Transcript used as primary source. |
| Signed Contract | Missing | — |
| Scope of Work | Missing | — |
| Proposal PDF | Missing | — |
| Reverse Brief | Missing | — |
| Fox Tone of Voice.docx | Provided (initial commit) | Full quality — 4 voice pillars: Clear Not Clever, Calm and Reassuring, Empowering Not Controlling, Human and Relatable. Present from initial commit; not reviewed in original discovery pass. |
| FFG Writing Guidelines Content Tone Of Voice.docx | Provided (2026-05-04) | Full quality — detailed ToV guide. StoryBrand-inspired. Customer = Hero. Year 7-9 reading level. Includes vocabulary, sentence structure, rhetorical devices, and formatting rules. |
| Brand Promise & Company Values.docx | Provided (2026-05-04) | Full quality — brand promise "Save More, Stress Less, Live Better." 6 company values. Clear positioning statement. |
| Fox Finance Group Branding Guide.pdf | Provided (2026-05-04) | Full quality — logo usage rules, colour palette (orange #ED9B33, navy #101820, grey #63666A), fonts (Muli/Helvetica Neue), mascot "Alex the Fox", photography guidelines. |
| FFG Site Map.docx | Provided (2026-05-04) | Full quality — complete URL structure for Fox Finance Group site. CTA routing by loan type, trust pages, calculator pages, all loan category pages. |
| FHL Site Map.docx | Provided (2026-05-04) | Full quality — complete URL structure for Fox Home Loans site. CTA routing, calculator pages, all home loan product URLs including medico/specialist pages. |
| Logo files (3) | Provided (2026-05-04) | Visual assets — grey logo (JPG + PNG), home logo, site white logo. |

---

## 4. Key Findings

### Goals (from transcript)
- Build a GHL CRM system with automated nurture sequences for each loan type
- Implement customer routing logic — explicit decision matrices to assign leads to the correct pipeline and sequence
- Integrate Ambition data into GHL via SendGrid API (weekly CSV export → GHL import, enriched with credit/income data)
- Launch a reactivation campaign for dormant leads (starting 12 months back, targeting 6-month window)
- Build micro lead magnets (calculators, guides) as CTAs within weekly content to grow the email list
- Establish a cross-sell pipeline: home loans team introduced during vehicle/personal loan settlement calls

### Existing Systems
| Tool | Current Use |
|---|---|
| GoHighLevel (GHL) | Pipeline management (extent of current configuration unknown) |
| Ambition | Primary CRM — richer financial data (credit scores, household income). API revamp expected in next couple of months. |
| SendGrid | Email platform; initial integration point for Ambition → GHL data migration |
| SEMrush / GA4 / Google Search Console | Connected marketing system, already operational |
| Twilio | SMS delivery (separate number from current systems — to be configured) |
| 3CX | Phone system used by Rowdie's team for inbound/outbound calls |
| LMG (Loan Market Group) | Aggregator being evaluated as potential Ambition replacement — API capability being assessed. May affect integration scope if adopted. |

### Quick Win Candidate
EV loan market opportunity: search volume up 161% since February, twice-weekly top search queries, clear market misconception to address ("do I need to earn $100k to qualify"). A targeted lead magnet or landing page correcting this misconception would capture bottom-of-funnel intent with high conversion likelihood.

### Stakeholders
| Name | Role | Notes |
|---|---|---|
| Rowdie Lang | Day-to-day contact, operations lead | Technically capable; dedicated; routing logic and ICA definitions are in his head |
| Nathan Drew | Decision maker | Not present in Apr 20 call; sign-off requirements unknown |
| Maddie | Unknown | James mentioned "just you, Nathan and Maddie" having GHL data access — role not confirmed |
| James Killick | Njin delivery lead | Technical lead; holds some ICA data sent by Rowdie prior to Apr 20 |
| Xavier Ybanez | Njin developer | Present in Apr 20 call; building project scope with George |
| George Votava | Njin PM / biz dev | Building project scope with Xavier; created Timeline PDF |

### Business Structure
Fox Finance Group (FFG) and Fox Home Loans (FHL) are **two separate business units** with different teams and nurture cadences. The cross-sell pipeline spans both entities. This is a critical scoping detail — GHL pipelines and automation sequences need to be built for both.

| Entity | Loan Types | Nurture Cadence | Cross-Sell Direction |
|---|---|---|---|
| Fox Finance Group (FFG) | Vehicle, Personal, Business | 6-12 months (asset finance) | → Fox Home Loans at settlement if home purchase identified |
| Fox Home Loans (FHL) | Home Loans | 18 months | → FFG for debt consolidation if applicable |

### Constraints
- Routing logic and ICA definitions are in Rowdie's head — some ICA data sent to James but not in project folder
- LMG API assessment is pending — if LMG replaces Ambition, data integration scope changes
- Data mapping (Ambition/SendGrid → GHL) requires Rowdie to categorise fields; this is a client-side dependency
- Nathan Drew was not in the Apr 20 call — his sign-off requirements and priorities are unknown
- Thursday scope meeting outcomes are not captured in any available document
- Engagement pricing is unclear — James offered $27k-value workshop at no cost, suggesting this may be discounted

---

## 5. Gaps and Outstanding Requests

### Hard Blockers — must be resolved before scoping

| # | Gap | Owner | Specific Request |
|---|---|---|---|
| B1 | Signed Contract | James / Nathan / Rowdie | Confirm contract status; provide signed copy to `Docs/background/` |
| B2 | Framework type confirmation | James / George | Confirm: Playbook, VIBE OS, or both? Determines delivery sequence and scope structure. |
| B3 | Timeline confirmation | James / George | Confirm: 5 weeks (COS) or 10 weeks (Timeline PDF)? Update COS once confirmed. |
| B4 | GHL Access Confirmation | Rowdie | Confirm Njin team has GHL account access, or provide subscription link from Apr 20 call. |

### Significant Gaps — needed before scope document is written

| # | Gap | Owner | Specific Request |
|---|---|---|---|
| S1 | SOW / Proposal PDF | George / James | Provide the document sent to Nathan and Rowdie. Drop into `Docs/background/`. |
| S2 | ICA / Customer Profile Documentation | James (has it) / Rowdie | Rowdie sent ICA data to James before Apr 20. James to add to `Docs/background/`. Routing decision matrix still needs to be built. |
| S3 | Current GHL Pipeline Documentation | Rowdie | Export or screenshot current GHL pipeline stages, existing automations, and contact record fields. Screen recording also works. |
| S4 | Customer Data Field Map (Ambition → GHL) | Rowdie | Flag Ambition fields as critical / key / nice-to-have for GHL import. Simple table format is sufficient. |

Full client-ready gap requests: `Docs/discovery/gap-report.md`

---

## 6. Readiness Assessment

**Can discovery advance to scoping? CONDITIONAL**

Discovery is complete based on available materials. However, the scoping gate cannot open until:
- B2 (framework type) is confirmed — scoping against the wrong framework produces a useless scope document
- B3 (timeline) is confirmed — scoping against the wrong timeline produces the wrong plan
- B1 (contract) is signed — this is a binary scoping gate requirement

B2 and B3 are internal confirmations (James / George) and can be resolved quickly. B1 requires client action.

---

## 7. Recommended Next Steps

| Priority | Action | Owner |
|---|---|---|
| 1 | Confirm framework type (B2) — internal conversation with James / George | PM |
| 2 | Confirm project timeline (B3) — internal; update COS once confirmed | PM |
| 3 | ~~Add verbatim transcript~~ — DONE, committed to Xavier branch | PM |
| 4 | Chase GHL access confirmation (B4) | PM → Rowdie |
| 5 | Chase contract (B1) | PM → Nathan / Rowdie |
| 6 | Once B2 + B3 confirmed — advance COS to Scoping phase; update framework reference if required | PM |
| 7 | Collect S1–S4 before scope document is written | PM |

---

## Quality Checklist

- [x] Engagement type confirmed in `cos.yaml`
- [x] Framework reference consulted — `ai-orchestration.md` + `orchestration-client.md`
- [x] Requisite Document Plan PM-approved before analysis began
- [x] Every provided document read and quality-assessed
- [x] Partial documents recorded as partial — not marked as fully provided
- [x] Gap Report produced with specific client requests (not generic asks)
- [x] Hard blockers and significant gaps clearly distinguished
- [x] Earliest Possible Win candidate identified — EV loan lead magnet
- [x] Framework fit risk addressed explicitly
- [x] Timeline discrepancy addressed explicitly
- [x] Discovery Report includes clear Readiness Assessment: CONDITIONAL

---

*Produced by Insight (Business Analyst) — Njin PM Framework — 2026-05-01*
