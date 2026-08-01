# Fox Finance Group - Claude Code Configuration

This file provides guidance to Claude Code when working in this project.

## Project Overview

**Client:** Fox Finance Group (FFG), Fox Home Loans (FHL) & UMI Loans (UMI)
**Industry:** Financial services (asset finance + home lending + sub-prime secured lending)
**Offer Package:** Cross-selling & Monetisation Playbook + Pre-sales SDR Playbook, delivered via GHL + integrations with existing providers
**CRM Platform:** GoHighLevel (GHL) with integrations to Fox's existing providers. POLR custom build paused per Apr 16 Mati decision — may resume if GHL implementation surfaces gaps.

## Framework

This project uses the **Njin Method** - a revenue-first AI transformation framework.

### Key Files

- `cos.yaml` - Client Operating System (Single Source of Truth). Read before every decision.
- `playbooks/master-playbook/tone-of-voice.md` - Brand voice guide. All content must match documented voice. **STATUS: v1.0 CREATED (2026-03-05). Gate PASSED.**

### Hidden Folders

- `.njin-method/` - Framework documentation, templates, tasks, workflows
- `.claude/` - Agents, skills, and commands

## Project Structure

```
Fox/
├── cos.yaml                 # Client Operating System
├── playbooks/master-playbook/tone-of-voice.md         # Brand voice guide (created during Activation)
├── docs/                    # Documentation
│   ├── discovery/           # Briefing docs, discovery data, referrer context, meeting transcripts
│   ├── baseline/            # Baseline metrics and data (FFG + FHL)
│   ├── strategy/            # ICAs, one-pagers, customer journey, vision docs, immersion analysis
│   ├── branding/            # Branding guide + tone of voice (first draft)
│   ├── edms/                # EDM automations (content + engagement stats)
│   ├── research/            # Market research
│   └── updated-docs/        # Working docs — FFG sales scripts, call processes, FHL lifecycle
├── playbooks/master-playbook/  # master playbook
├── crm/                     # CRM configuration
├── training/                # Training materials
├── assets/                  # Creative assets
├── data/                    # Analytics and exports
└── deliverables/            # Client-facing deliverables
```

## Working Principles

### COS-First Protocol

1. **Read `cos.yaml` before every decision** - It contains the 12 Core Numbers, constraint diagnosis, TORQUE phase, and blocking gates
2. **Update `cos.yaml` after every meaningful change** - Add to change_log with phase context
3. **Check status and blockers** - Yellow/Red health means address blockers first

### Blocking Gates

Before creating content, verify these gates are passed:

1. **Tone of Voice** - `playbooks/master-playbook/tone-of-voice.md` must exist
2. **Data Access** - CRM access must be granted
3. **Baseline Validated** - 12 Core Numbers confirmed with real data
4. **Stakeholder Approval** - Strategy approved by client
5. **Immersion Complete** - Week 1 discovery finished

### Revenue-First Routing

Route work based on constraint diagnosis:

| Constraint | Focus Area |
|------------|------------|
| Acquisition | Lead generation, ads, outreach |
| Conversion | Nurture, qualification, closing |
| **Monetisation** | **Cross-sell, upsell, pricing** |
| Retention | Churn prevention, referrals |

**Primary constraint: Monetisation** - Three businesses (FFG, FHL, UMI) operating in silos with no unified customer view or systematic cross-sell. Playbooks are delivered via GHL with integrations to Fox's existing providers (POLR custom platform paused per Apr 16 Mati decision).

### TORQUE Phases

| Phase | Focus |
|-------|-------|
| Transform | Define transformation (completed) |
| **Observe** | **Validate data, collect access (current phase)** |
| Roadmap | Plan implementation |
| Qualify | Create methodology, pilot (Weeks 1-6) |
| Upgrade | Train team, full rollout (Weeks 7-12) |
| Evolve | Ongoing success |

## Available Agents

Access agents via `.claude/agents/`. Key agents:

- **Orchestrator** - Central coordination hub
- **Qualification Analyst** - Pre-sale diagnostics
- **Activation Specialist** - Post-sale setup
- **Fulfilment Specialists** (7) - Playbook creation by constraint
- **Tone of Voice Agent** - Brand voice extraction
- **CRM Agent** - CRM automation
- **Developer** - Code-based implementations

## Available Skills

Skills transfer expert-level thinking patterns:

- `cos-structure-expert` - COS YAML structure expertise
- `voice-scoring-expert` - Content voice validation
- `playbook-structure-expert` - playbook methodology
- `constraint-diagnosis-expert` - Revenue constraint analysis
- `competitive-ads-extractor` - Competitor ad analysis

## Quick Commands

```
/cos view         # View COS summary
/cos update       # Update COS fields
/phase            # Check current TORQUE phase
/health           # Check health status
/voice-check      # Validate content against voice
/constraint       # Review constraint diagnosis
```

## Writing Standards

- **Language:** Australian English (organisation, colour, analyse)
- **Reading Level:** Third-grade for clarity
- **Formatting:** No EM dashes in content
- **Voice:** Advisory, guiding, trustworthy. StoryBrand framework (customer = hero, Fox = guide). Human-led approach for cross-sell messaging.
- **Compliance:** Never use "advice", "guarantee", or "financial hardship" in client-facing content.

## Client Communications — Zero Fabrication Rule

**NEVER make anything up in client communications. Ever.**

Client comms = anything that could be sent to, shown to, or read by Fox. Includes: agendas, recap emails, proposals, decks, scripts, meeting notes, status updates, scope docs, names, titles, dates, numbers, quotes, decisions, commitments.

**The rule:**
- Every name, surname, title, email, number, date, quote, decision, or commitment in a client-facing artefact MUST come from a verified source: cos.yaml, a Fathom transcript, an email in the thread, a doc in `/docs/`, or something James said in this session.
- If the source does not exist or is unclear → **ask James or leave it blank**. Never fill the gap with a plausible guess.
- If unsure whether something is verified → flag it explicitly ("I don't have a source for X — confirm?") before writing it.
- Plausibility is not verification. "Nathan Lopez" sounds like a real name. It was invented. That is a hard fail.

**Why:** A single fabricated detail in client comms erodes trust, embarrasses Njin, and is hard to walk back. The cost of pausing to ask is low. The cost of inventing is high.

**Verified Fox stakeholder names:**

Primary contacts:
- Rowdie Lang (Operations & Marketing, day-to-day Njin contact)
- Nathan Drew (MD / Business Owner across FFG/FHL/UMI)

Fox broker / lending team (verified in cos.yaml `ownership.team`):
- Bill Robb (Head of Home Loans / Partnerships, FHL)
- Sam Drew (Head of Asset & SME, FFG)
- Paige Beveridge (Home Loan Lending Specialist, FHL)
- Angel (Lending Specialist, FHL, added 2026-03-06)
- Andrew Glen (Lending Specialist, FFG)
- Bradley Robb (Lending Specialist, FFG)
- Brad (Top Performing Broker, FFG)
- Jess (Lending Specialist)
- Mason (Operations Manager, UMI)
- Ben (Marketing)

Njin team:
- John Xavier Ybañez (PM)
- George Votava (oversight)
- James Killick (lead)

**Rule:** Before generalising or flagging any name as unverified, check this list AND cos.yaml `ownership.team` + `ownership.njin_contacts`. Only ASK if the name is missing from both.

---

*Generated by Njin Method Framework v2.0*

<!-- BEGIN AUTO-MANAGED: agent-index (regenerated by deploy-claude-structure.sh) -->
## Deployed Agents & Skills

Full registries: [agents](.claude/agent-registry.md) · [skills](.claude/skill-registry.md)
<!-- END AUTO-MANAGED: agent-index -->

<!-- BEGIN AUTO-MANAGED: cos-discipline (regenerated by deploy-claude-structure.sh) -->
## COS Update Discipline

`cos.yaml` is the single source of truth for this engagement. The `cos-update` skill keeps it that way. See `.claude/skills/cos-update/SKILL.md` for the full spec.

**Auto-fire `cos-update` when the conversation contains any of these:**

| Trigger phrase | Action |
|---|---|
| "we decided / X is locked / decision finalised / joint decision" | Append change_log entry tagged `decision_logged` |
| "blocker / blocking / paused / parked / shelved" | Append change_log + push to `status.blockers[]` |
| "X resolved / X passed / unblocked / cleared" | Append change_log + remove from blockers |
| "kickoff / pivot / strategic pivot / scope locked" | Append change_log + update `status.health` |
| "inputs delivered / received [doc] / [name] sent" | Append change_log entry tagged `input_received` |
| "next milestone / target date / due [date]" | Append change_log + update `status.next_milestone` |
| "ToV passed / data access granted / gate passed" | Append change_log + flip `gates.<name>` |
| Meeting transcript / Fathom summary processed in-session | Append change_log with sections_affected + source_documents |

**Auto-fire on entering this client.** When session opens work here, check `status.last_updated`. If > 14 days, ask once: "cos.yaml hasn't moved since [date]. Anything to log from since then?" Then run `cos-update`.

**Don't fire when:**
- Discussion is portfolio-level or cross-client.
- The same change is already in change_log within last 7 days.
- The cos.yaml is brand-reference shape (no `status.blockers`, no `change_log`). Skill auto-skips.
- The user says "don't log this" or "off the record".

**Honest confirmation only.** Path A (surgical YAML edit) → Path B (Bash append fallback) → Path C (abort + paste yourself). Never fabricate "saved".
<!-- END AUTO-MANAGED: cos-discipline -->

<!-- BEGIN AUTO-MANAGED: ai-os-wiki (regenerated by AI-stack scripts/wiki_claude_block.py; do not hand-edit) -->
## AI OS Wiki

A persistent, interlinked wiki maps how the AI Operating System fits together (frameworks, skills, MCPs, plugins, the internal team, methodologies, decisions) and why. Synthesis is done at ingest, not at query. Use it before re-deriving how things connect.

- **Query for relationship and "why" questions.** "How does X connect to Y", "what depends on Z", "why is this set up this way", "where does X fit", "the map". Use the `wiki-query` skill. It reads `index.md` and `ROUTING.md` first, then the wiki search (SQLite FTS, plus Pinecone where the scope has it). Do not hand-derive a link the wiki already records. (`/recall` is the separate session-memory plane, not the wiki, see below.)
- **Feed it when work produces durable structure.** A new framework, skill or decision, a non-obvious link, a settled answer worth keeping: hand the source to the `wiki-ingest` skill. Session capture is automatic (SessionEnd and PreCompact). Never hand-edit `wiki.db` or Pinecone. The markdown pages are the truth.
- **Flat "where is X / do we have X / is X installed" stays manifest-first.** Those are exact inventory lookups, not relationship questions. Grep the AI-stack manifest first. The wiki answers how and why, not what-exists.

Four scopes, isolated by path identity (never trusted from config):

| Scope | Where | Pinecone |
|---|---|---|
| central | `AI-stack/wiki/` | `ai-stack` ns `ai-wiki` |
| team | `{Project Management,Sales,Marketing,Content}/.wiki/` | `ai-stack` ns `team-<slug>` |
| client | `Clients/<C>/.wiki/` | none |
| project | `Clients/<C>/<p>/.wiki/` | none |

A deployed client or project wiki is local markdown plus SQLite only. It never reaches Pinecone, never acts central or team, and never crosses to another client. This project's wiki, if present, is at `.wiki/`. Two planes never collide: the wiki-page plane (`ai-stack`) and the session-memory plane (`ai-os-memory`, written by `/wrap`, read by `/recall`).
<!-- END AUTO-MANAGED: ai-os-wiki -->
