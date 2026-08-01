# Njin Method Framework Update — Handoff Prompt

**Source engagement:** Fox Finance Group (fox-njin)
**Date:** 2026-05-15
**Reason:** Two rounds of feedback on the pre-sale developer guides (07c) and cross-sell developer guides (07e) exposed structural and content patterns the framework should enforce, not regenerate. The framework needs to learn so the next client doesn't get the same first-draft mistakes.

---

## Mission

Update the Njin Method framework (templates, agents, skills, the master playbook generator) so future client engagements produce playbooks that:

1. Match Fox's actual operating model (real stages, real handoffs, real touch counts).
2. Avoid the verbose, over-engineered, theoretical content patterns the framework currently defaults to.
3. Use the new structural primitives proven in the Fox build (linked T-stages, numbered UTM slots, simpler scripts, "Rowdie to advise" placeholders for unknowns).

---

## Hard Rules the Framework Must Enforce

### 1. Pre-sale pipelines never include Engaged, Qualified, or Booked Out stages

- **Why:** `Engaged` duplicates `Interacting`. `Qualified` and `Booked Out` are not pipeline stages — they are events. Booked = card exits to Closer Pipeline.
- **Enforce in:** every pre-sale developer guide template, every pipeline architecture section, every Red Dot Protocol SLA table.
- **Valid pre-sale pipeline shape:**
  - `Interacting` (➡️ ⚡️)
  - `FUP` (👤)
  - Linked T-stages (see rule 2)
  - N-series nurture block (single stage)
  - Card exits to Closer Pipeline on booking. No exit stage.
- Any reply at any T or N stage moves the card BACK to `Interacting`. Not "Engaged".

### 2. T-system stages must be grouped, not one-per-touch

- **Why:** Consecutive auto touches and consecutive manual touches belong in one pipeline stage. Splitting every touch into its own kanban column creates visual noise and breaks the broker's mental model.
- **Pattern (use this shape):**
  - `T1-T2` (auto pair, Day 1)
  - `T3-T5` (manual call attempts, Day 1)
  - `T6` (auto pair)
  - `T7-T8` (manual)
  - `T9` (auto)
  - `T10-T11` (manual)
  - `T12` (auto pair)
  - `T13` (manual final call)
  - `T14` (auto breakup)
- Only break a group when there is a real time gap or channel switch.
- Adapt the cadence shape per brand (FHL is 16 days, FFG is 4 days) but keep the linking principle.

### 3. Only T1 and T2 vary by input

- **Why:** Variant content beyond T1/T2 explodes the maintenance surface for zero meaningful conversion lift.
- **Enforce:** T1 (email) and T2 (SMS pair) can have a magnet variant or Purchase Type variant. T3 onwards is the same regardless of input.
- The framework should reject draft playbooks that put input-driven variants at T6, T9, T12, N-series, etc.

### 4. T2, T6, and the late-cadence breakup SMS are SMS pairs, not single sends

- **Why:** Splitting the intro and the call-ask into two consecutive SMS reads more human and lets the second carry the actual ask.
- **Pattern:**
  - T2a: `Hey {first_name}, {sdr_name} from {brand}. Got your enquiry.`
  - T2b (5 min later): `Want me to give you a call shortly? Reply YES and I will.`
  - T6a: `Hey {first_name}, tried to reach you today again about your enquiry.`
  - T6b: `{first_name}, would you like to proceed through SMS?`
  - T12a (FFG only): `You just got a call from me.`
  - T12b: `If you'd still like to chat, give me a quick reply.`

### 5. UTM tracking uses numbered slots, not append-only history

- **Why:** A `utm_history` long-text field is a graveyard. Numbered slots let downstream automations read the journey.
- **Enforce shape:**
  - Opportunity: single trio (`utm_medium`, `utm_source`, `utm_campaign`).
  - Contact: `utm_1` (first touch, locked) + `utm_2`, `utm_3`, `utm_4`, `utm_5` for subsequent touches.
  - `utm_5` is last-touch-wins once full.

### 6. "Broker Handoff" / "Broker Assignment" sections must NOT invent process

- **Why:** Most clients haven't documented their broker handoff process. Inventing one means the playbook describes a fantasy.
- **Default content when undocumented:** `"[Owner name] to advise. Process for moving a booked lead from the pre-sale pipeline into broker ownership has not been documented yet."`
- The framework should refuse to generate a "Round-robin guardrails" / "Assignment rules priority order" section unless the source data names a documented process.

### 7. No empty placeholder blocks

- **Why:** A `## Rowdie Input Needed` block with a single TBD row is noise. If there's no content, the section shouldn't render.
- **Rule:** placeholder sections only ship when populated. Empty TBD rows = section omitted.
- Track open questions in cos.yaml `status.blockers[]` or `change_log`, not inside the playbook body.

### 8. Sections to never auto-generate

The framework currently generates these by default. They add bulk and rarely survive client review. Remove from default templates:

- `Funnel Baseline` section that duplicates section 1-4 numbers
- `Lead Sources and Routing` table (replaced by UTM Tracking)
- `T-Series: Direct Cadence` table that duplicates the pipeline stage table
- `Variable-Field Branching (ICA-Driven Copy)` / `{ica_hook}` merge token system
- `Worked T2 SMS example per ICA` table
- `Reporting Hooks` / `Reporting Dashboard` section (developer guides)
- `Build Order` / `Build Sequence` section
- Optional name-drop emails using `{client_story_name}` / `{client_story_situation}` / `{client_story_outcome}` fields

If a client wants any of these later, add them deliberately. Don't ship them by default.

### 9. Script content lives in fenced code blocks

- **Why:** Email and SMS copy in bullet lists is unreadable when there are merge tokens, line breaks, or subject lines.
- **Rule:** every email body, SMS body, and voicemail script in a playbook must sit in a ` ``` ` block. Variant content (per magnet, per Purchase Type) gets its own block.

### 10. No "too much introduction" in T1

- **Why:** The current T1 email template generates 5+ paragraphs explaining what Fox does, what to expect, etc. Real Fox openers are 3 lines.
- **Target T1 shape:**
  - One line greeting + acknowledge enquiry.
  - One line action ("I'll give you a quick bell shortly.").
  - Signature block.
- The framework should cap T1 at ~6 lines of body.

### 11. Don't separate "general path" and "lead magnet path" as parallel sections

- **Why:** Parallel sections force a reader to flick between two near-identical flows. Rolling text + variant snippets reads cleaner.
- **Rule:** one cadence narrative. T1 and T2 expose variants in-line. T3 onwards is shared content with no branching.

---

## Soft Rules (Style / Voice)

- **No em dashes anywhere.** Already in the master voice rules — flag if any generator output contains one.
- **Australian English.** Already enforced.
- **No filler intros** ("In today's fast-paced world..."). Already enforced.
- **CTA pattern:** "Reply YES and I will." style, not "let me know your thoughts".
- **Sign-off:** `Cheers,` + name + brand. Not `Best regards`.

---

## Concrete Files to Update in the Framework

The Njin Method framework lives at `/Users/jameskillick/Documents/Projects/Frameworks/Njin-Method/` (or wherever the current source-of-truth lives — check first).

Likely touchpoints:

| Framework file | What to change |
|---|---|
| Master playbook template for `07c-pre-sales-developer-guide.md` | Apply rules 1-11 above to the default scaffold |
| Master playbook template for `07e-cross-sell-developer-guide.md` | Apply rules 5, 7, 8, 9 (cross-sell doesn't use T-system) |
| `fulfilment-specialist` agent (pre-sales variant) | Lint against rules 1-11 when generating |
| `playbook-structure-expert` skill | Add the linked-T-stage primitive + UTM numbered slot primitive |
| `voice-scoring-expert` skill | Already enforces voice rules — confirm em-dash detection is active |
| `cos-structure-expert` skill | Add convention: open questions live in `status.blockers[]`, not in playbook body |

Document the rules in the framework's own CLAUDE.md or rules folder so future agents inherit them without needing this prompt.

---

## What the Framework Should Reject

When a draft playbook is generated, the framework should flag (or auto-correct) any of these:

- Pipeline stage tables containing `Engaged`, `Qualified`, or `Booked Out`
- T-series pipeline tables with every touch as its own stage (no grouping)
- `utm_history` field definitions (use numbered slots instead)
- `## Reporting Hooks` / `## Reporting Dashboard` / `## Build Order` / `## Build Sequence` sections in dev guides
- `{ica_hook}` / `{pt_hook}` / `{client_story_*}` merge tokens in scripts
- Bullet lists of script variants (must be fenced blocks)
- T1 email bodies longer than ~6 lines
- Broker handoff sections with invented assignment rules when the source data names no documented process
- Empty TBD placeholder blocks ("Rowdie Input Needed" with one TBD row)

---

## Reference: Files Modified in the Fox Engagement

For the receiving agent to study the new patterns, the canonical reference files (post-feedback) are:

- `/Users/jameskillick/Documents/Projects/Clients/Fox/fox-njin/playbooks/master-playbook/ffg/07c-pre-sales-developer-guide.md`
- `/Users/jameskillick/Documents/Projects/Clients/Fox/fox-njin/playbooks/master-playbook/fhl/07c-pre-sales-developer-guide.md`
- `/Users/jameskillick/Documents/Projects/Clients/Fox/fox-njin/playbooks/master-playbook/ffg/07e-cross-sell-developer-guide.md`
- `/Users/jameskillick/Documents/Projects/Clients/Fox/fox-njin/playbooks/master-playbook/fhl/07e-cross-sell-developer-guide.md`

The 07c files are the cleanest reference for the new pre-sale shape. The 07e files show the cross-sell variant (different pipeline model, same UTM + Rowdie / Reporting / Build Sequence philosophy).

---

## Definition of Done

The framework update is done when:

1. The 11 hard rules above are encoded in the relevant templates, agents, and skills.
2. A test generation of a new client's `07c-pre-sales-developer-guide.md` from scratch produces output that matches the Fox post-feedback shape without manual cleanup.
3. The framework's CLAUDE.md or rules folder documents the anti-patterns so future agents inherit the rules.
4. cos.yaml convention updated: open client questions live in `status.blockers[]`, not in playbook bodies.

---

*End of handoff. The receiving agent should read the Fox 07c files first, then update the framework templates and agent prompts to enforce the rules above.*
