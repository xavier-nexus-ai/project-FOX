# Requisite Document Plan
**Client:** Fox Finance Group Pty Ltd
**Engagement Type:** orchestration (framework fit under review — see flag below)
**Framework Reference:** `methodology/frameworks/ai-orchestration.md` + `methodology/project-types/orchestration-client.md`
**Produced by:** Insight (Business Analyst)
**Date:** 2026-05-01
**Status:** PM APPROVED — 2026-05-01

---

## Critical Flags

### Flag 1 — Framework Fit Risk
The Apr 20 transcript and PM confirmation describe this engagement as: *creating a playbook then implementing it in GHL for CRM build and workflow automation.* This is a two-part engagement:
1. **Playbook creation** — documenting the Fox Finance delivery process as a structured guide
2. **GHL implementation** — building CRM workflows, automation, and nurture sequences

This does not match pure AI Orchestration (IP extraction into AI agents). It is closer to a **Njin Playbook + VIBE OS hybrid**. Framework type must be confirmed with James Killick and George Votava before scoping begins. If confirmed as a different engagement type, document requirements and delivery sequence will change.

### Flag 2 — Timeline Discrepancy
| Source | Timeline |
|---|---|
| `cos.yaml` `target_completion` | 5 weeks (ends 2026-06-05) |
| Timeline PDF (PM confirmed) | 10 weeks |

These conflict. PM must confirm the correct timeline with James / George before scoping. COS must be updated once confirmed.

---

## Requisite Document Plan

| # | Document / Artefact | Required For | Status | Source |
|---|---|---|---|---|
| 1 | Signed Contract | Scoping gate cannot pass without it | MISSING | Client — Nathan Drew / Rowdie Lang |
| 2 | Scope of Work (SOW) | Defines what was sold; required to verify framework alignment | MISSING | Njin Sales |
| 3 | Proposal PDF | Confirms deliverables and pricing agreed | MISSING | Njin Sales |
| 4 | Reverse Brief | Client's interpretation of the engagement; validates alignment before scope is written | MISSING | Client |
| 5 | Sales Call Transcript — Apr 20 2026 (AI summary) | Primary source for client goals, context, and existing systems | PROVIDED — partial quality (AI-generated meeting summary with timestamps; ~42 mins condensed to ~600 words; nuance likely lost) | Sales |
| 6 | Sales Call Transcript — Apr 20 2026 (verbatim) | Higher-quality source for gap analysis | PROVIDED — full quality. 42-minute verbatim transcript confirmed. Supersedes AI summary. | Sales |
| 7 | Operational Master Document | Business context: loan pillars, 5-step SOP, assessment framework | PROVIDED — partial quality (4 sections only; covers core process but missing team structure, revenue data, existing GHL configuration, full workflow documentation) | Client |
| 8 | Timeline / Project Plan PDF | Engagement milestones, project duration, delivery phases | PRESENT BUT UNREADABLE — image-based PDF; text cannot be extracted. PM confirmed content: 10-week project plan | George Votava |
| 9 | GHL Access Confirmation | Required before any build work begins; confirms team can access live GHL account | MISSING | Client — Rowdie Lang |
| 10 | Current GHL Pipeline Documentation | Documents existing GHL setup: pipelines, stages, automations, forms, tags, contact records | MISSING | Client |
| 11 | ICA / Customer Profile Documentation | Defines Ideal Customer Avatars for routing logic and nurture sequence design | MISSING — Rowdie's action item from Apr 20 call | Client — Rowdie Lang |
| 12 | Customer Data Field Map (Ambition → GHL) | Required for data integration scope; Rowdie to flag critical / key / nice-to-have fields | MISSING — Rowdie's action item from Apr 20 call | Client — Rowdie Lang |
| 13 | Existing Nurture Sequences / Email Templates | Establishes baseline for automation build — building from scratch or updating existing? | MISSING | Client |
| 14 | Ambition CRM Data Structure / Export Sample | Source data for GHL integration; field structure required before mapping can be scoped | MISSING | Client |

---

## Document Count Summary

| Status | Count |
|---|---|
| Provided (full quality) | 1 |
| Provided (partial quality) | 2 |
| Present but unreadable | 1 |
| Pending (confirmed, not yet in folder) | 0 |
| Missing | 10 |

---

## Additional Documents Provided (Outside Original Plan)

Added to `Docs/background/` on 2026-05-04. These were not in the original requisite list but are useful for scoping and content/automation work.

| Document | Content | Relevance |
|---|---|---|
| `Fox Tone of Voice.docx` | Customer-facing voice guide. 4 pillars: Clear, Calm, Empowering, Human. Present from initial commit. | Tone of Voice Agent; nurture sequence copy |
| `FFG Writing Guidelines Content Tone Of Voice.docx` | Detailed ToV guide — StoryBrand-inspired. Customer = Hero, Fox = Guide. Year 7-9 reading level. | Content creation, email sequences, lead magnets |
| `Brand Promise_Company Values.docx` | Brand promise: "Save More, Stress Less, Live Better." 6 values: Integrity, Accountability, Collaborative, Productive, Knowledge, Connection. | Brand alignment; messaging for nurture sequences |
| `Fox Finance Group Branding Guide.pdf` | Logo usage, colour palette (orange #ED9B33, dark navy #101820, grey #63666A), fonts (Muli/Helvetica Neue), mascot "Alex the Fox", photography guidelines | Any designed deliverables; GHL branded assets |
| `FFG Site Map.docx` | Full URL map for Fox Finance Group site: CTA routing by loan type, trust pages, calculator pages, all loan category URLs | Lead magnet scoping; CTA mapping in automations |
| `FHL Site Map.docx` | Full URL map for Fox Home Loans site: CTA routing, calculator pages, all home loan product URLs | Cross-sell pipeline scoping; FHL nurture CTAs |
| Logo files (3) | Fox Finance Group grey logo (JPG + PNG), home logo, site white logo | GHL branded templates |

---

## PM Approval Record

- **Approved by:** PM (verbal confirmation)
- **Date:** 2026-05-01
- **Notes:** Framework fit and timeline discrepancy flagged. PM to follow up James / George for confirmation. Verbatim transcript to be added to `Docs/background/` when available.

---

*Produced by Insight (Business Analyst) — Njin PM Framework — 2026-05-01*
