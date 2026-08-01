# Fox Finance Group — Gemini CLI / Antigravity Entry Point

> **How this file works:** Gemini CLI and Google Antigravity do not auto-discover sub-agents. This file is the discovery mechanism. Agents live in `.claude/agents/` (canonical for both Claude Code and Gemini CLI). Load one by referencing its file path via the `@.claude/agents/<name>.md` lines below. Claude Code users open `CLAUDE.md` instead — they get the same agents via auto-discovery.

## Project Overview

**Client:** Fox Finance Group (FFG), Fox Home Loans (FHL) & UMI Loans (UMI)
**Industry:** Financial services (asset finance + home lending + sub-prime secured lending)
**Offer Package:** Cross-selling & Monetisation Playbook + Pre-sales SDR Playbook, delivered via GHL + integrations
**CRM Platform:** GoHighLevel (GHL) with integrations to existing providers

## Framework

This project uses the **Njin Method** — a revenue-first AI transformation framework built on the TORQUE methodology (Transform → Observe → Roadmap → Qualify → Upgrade → Evolve). Your job as an AI agent is to augment the human team and drive client revenue.

## Key Files

- `cos.yaml` — Client Operating System (Single Source of Truth). Read before every decision.
- `playbooks/master-playbook/tone-of-voice.md` — Brand voice guide. All content must match the documented voice (BLOCKING gate; v1.0 PASSED 2026-03-05).
- `CLAUDE.md` — Claude Code entry point (same project context, same agents).
- `.claude/agents/` — Canonical agent directory.
- `.claude/skills/` — Canonical skills directory (loaded via `@.claude/skills/<skill>/SKILL.md`).
- `.claude/workflows/` — Phase execution sequences.
- `.njin-method/` — Framework reference (docs, templates, tasks, config).
- `.tmp/` — Workbench for intermediate files, scratch scripts, log outputs.

## Available Agents

> **Regenerate this block whenever an agent is added, removed, or renamed.**

- @.claude/agents/activation-specialist.md — Run activation call, validate baseline data, enforce data access gate (Observe + Roadmap)
- @.claude/agents/ads-specialist.md — Acquisition via Paid Advertising playbook (hooks, creative, audience optimisation)
- @.claude/agents/architect.md — System architecture, CRM integration, multi-platform playbook design
- @.claude/agents/chatgpt-ads-agent.md — ChatGPT/SearchGPT advertising strategy (intent-based monetisation)
- @.claude/agents/coach.md — Njin Method training, TORQUE/COS/playbook explanation, agent routing help
- @.claude/agents/conversion-specialist.md — Pre-TORQUE: close prospects into paying clients (sales scripts, proposals, objection handling)
- @.claude/agents/crm-agent.md — CRM configuration, workflow automation, pipeline setup
- @.claude/agents/cross-sell-specialist.md — Monetisation playbook (cross-sell/upsell, purchase prediction, expansion)
- @.claude/agents/customer-success-am.md — Ongoing client relationship management (TORQUE Evolve)
- @.claude/agents/data-analyst.md — Data requirements, lead scoring, KPI frameworks, dashboard specs
- @.claude/agents/developer.md — Custom code beyond CRM native: APIs, dashboards, chatbots
- @.claude/agents/domain-expert.md — Industry-specific playbook adaptation, compliance validation
- @.claude/agents/ethicist.md — Ethical impact, bias review, privacy evaluation for AI components
- @.claude/agents/facebook-ads-sub-agent.md — Meta-specific campaign structure and creative strategy
- @.claude/agents/fulfilment-specialist.md — Playbook strategy/delivery during Qualify and Upgrade (7 sub-specialisations)
- @.claude/agents/google-ads-sub-agent.md — Google Ads campaign structure, bidding, optimisation
- @.claude/agents/hormozi-coach.md — Blunt Hormozi-style diagnosis and routing (offers, leads, sales, retention)
- @.claude/agents/initialization-agent.md — One-time project setup; deploys structure, creates COS, validates
- @.claude/agents/linkedin-ads-sub-agent.md — LinkedIn B2B campaign structure and lead generation
- @.claude/agents/marketing-specialist.md — Supporting role: content, brand, funnel, SEO/GSO, GTM, growth
- @.claude/agents/operations-specialist.md — Encode playbook into daily/weekly/monthly execution rhythms
- @.claude/agents/orchestrator.md — Central coordination hub; phase routing and agent dispatch
- @.claude/agents/outreach-specialist.md — Acquisition via Cold Outreach playbook (multi-channel sequences)
- @.claude/agents/pre-sales-specialist.md — Conversion via Lead Nurture playbook (conversational AI, scoring, speed-to-contact)
- @.claude/agents/product-manager.md — Scope governance for custom scope changes / hybrid project requirements
- @.claude/agents/project-manager.md — Capacity management, multi-playbook coordination, sprint planning
- @.claude/agents/prompt-engineer.md — Prompt plans and production prompts for automation workflows
- @.claude/agents/qualification-analyst.md — New prospect qualification, discovery, constraint diagnosis (TORQUE Transform)
- @.claude/agents/referral-specialist.md — Retention via Referral Generation playbook
- @.claude/agents/retention-specialist.md — Retention via Churn Prevention playbook (health scoring, intervention)
- @.claude/agents/sales-specialist.md — Conversion via Closing playbook (objection detection, sentiment, scripts)
- @.claude/agents/skill-invocation-protocol.md — Njin Method skill invocation protocol
- @.claude/agents/tone-of-voice-agent.md — Extract and document client brand voice (BLOCKING gate during Activation)
- @.claude/agents/ux-designer.md — UI design, dashboards, user flows, CRM interface optimisation

## Available Skills

Skills live in `.claude/skills/<skill-name>/SKILL.md`. Reference one by path, e.g. `@.claude/skills/hormozi-offer/SKILL.md`. Full registry: `.claude/skill-registry.md`. Routing rules for overlapping skills: `.njin-method/skill-routing.md`.

Key skills:
- @.claude/skills/cos-structure-expert/SKILL.md — COS YAML structure, validation, field relationships
- @.claude/skills/cos-update/SKILL.md — Auto-fire on real changes to log in cos.yaml; honest-confirm discipline
- @.claude/skills/constraint-diagnosis-expert/SKILL.md — 12 Core Numbers diagnosis to identify primary revenue leak
- @.claude/skills/playbook-structure-expert/SKILL.md — playbook methodology and dependencies
- @.claude/skills/voice-scoring-expert/SKILL.md — 11-dimension content voice validation
- @.claude/skills/voice-humaniser/SKILL.md — Rewrite AI text to sound human and on-brand (BLOCKING for AI-drafted content)
- @.claude/skills/handoff-protocol/SKILL.md — Multi-chat handoff orchestration between agents/sessions
- @.claude/skills/competitive-ads-extractor/SKILL.md — Extract/analyse competitor ads from Meta/LinkedIn libraries
- @.claude/skills/competitor-research/SKILL.md — Standalone competitor research document
- @.claude/skills/icp-builder/SKILL.md — Data-driven ICP definition from top-20% customers
- @.claude/skills/conversion-methodology/SKILL.md — Njin selling methodology: 5 offer tiers, decision tree, objections
- @.claude/skills/njin-quoting/SKILL.md — Njin pricing logic: services, packages, bundles, estimates
- @.claude/skills/proposal-generator/SKILL.md — Interactive Njin proposal HTML generator
- @.claude/skills/discovery-generator/SKILL.md — Interactive discovery meeting presentations
- @.claude/skills/conversational-ai/SKILL.md — n8n + GHL conversational AI for lead qualification
- @.claude/skills/reactivation-ai/SKILL.md — SMS reactivation for cold/dead leads
- @.claude/skills/referral-ask-ai/SKILL.md — Indirect-ask warm network referral AI
- @.claude/skills/red-dot-protocol/SKILL.md — Pipeline failsafe: stage-based timing, YELLOW/RED escalation
- @.claude/skills/lead-score/SKILL.md — Lead scoring model (Hormozi qualification framework)
- @.claude/skills/sales-script/SKILL.md — Full sales scripts: CLOSER + Onion of Blame + 55+ closes
- @.claude/skills/call-script-generator/SKILL.md — Lean role-specific call scripts (flow-based)
- @.claude/skills/cold-email-outreach-generator/SKILL.md — B2B cold email copy (2026 best practices)
- @.claude/skills/linkedin-outreach-generator/SKILL.md — LinkedIn warm/cold prospecting messaging
- @.claude/skills/cold-outreach-strategy/SKILL.md — Multi-channel outreach strategy (warm + email + LI + WA)
- @.claude/skills/nurture-content-generator/SKILL.md — Lead nurture sequences (Four Pillars, NEPQ, ACA)
- @.claude/skills/content-generator/SKILL.md — Web/email/social/sales content with voice enforcement
- @.claude/skills/content-strategy/SKILL.md — Content strategy: Hook-Retain-Reward, 70-20-10 testing
- @.claude/skills/content-calendar/SKILL.md — Rule of 100 content volume planning
- @.claude/skills/hook-generator/SKILL.md — Headlines, subject lines, scroll-stopping copy
- @.claude/skills/ads-ideas/SKILL.md — Ad concept generation (5 Meats, Marketing Machine)
- @.claude/skills/ads-trilogy/SKILL.md — Discovery-Consideration-Conversion ad funnel
- @.claude/skills/video-ad-hook/SKILL.md — Video ad hooks by awareness level
- @.claude/skills/vsl-creator/SKILL.md — VSL scripts (Hormozi 5 Ps + VSL Sandwich)
- @.claude/skills/reel-script-writer/SKILL.md — Short-form video scripts (Reels/TikTok/Shorts)
- @.claude/skills/funnel-page-builder/SKILL.md — Landing/opt-in/sales pages with scent matching
- @.claude/skills/sales-funnel-strategy/SKILL.md — Sales funnel architecture (VSL Sandwich + Money Model Flow)
- @.claude/skills/lead-magnet-builder/SKILL.md — 7-step lead magnet creation framework
- @.claude/skills/identity-framing/SKILL.md — Pre-call identity sequences for show-up rates
- @.claude/skills/brand-messaging/SKILL.md — Positioning + messaging architecture
- @.claude/skills/go-to-market-strategy/SKILL.md — Whisper-Tease-Shout launches, Fast Cash, Core Four
- @.claude/skills/growth-strategy/SKILL.md — Sustainable growth (Crazy Eight LTV, CFA, retention)
- @.claude/skills/seo-strategy/SKILL.md — Traditional SEO planning
- @.claude/skills/aso-strategy/SKILL.md — Agentic Search Optimisation (ChatGPT/Perplexity/Claude/Gemini visibility)
- @.claude/skills/instantly-coach/SKILL.md — Instantly.ai cold email setup, deliverability, AI features
- @.claude/skills/sales-enablement/SKILL.md — Pitch decks, one-pagers, objection handling, demo scripts
- @.claude/skills/sales-team-builder/SKILL.md — Hiring/onboarding/training sales teams (career progression)
- @.claude/skills/referral-program/SKILL.md — Referral/affiliate program design
- @.claude/skills/referral-partner-avatar/SKILL.md — Referral partner identification (access-based)
- @.claude/skills/ai-sdr-builder/SKILL.md — AI SDR design (DM/SMS/voice/email scripts)
- @.claude/skills/ai-orchestrator/SKILL.md — Multi-agent orchestrator design (n8n + Custom GPT)
- @.claude/skills/ai-agent-builder/SKILL.md — Custom GPT / Gem / Copilot design
- @.claude/skills/gpt-builder/SKILL.md — ChatGPT GPT creation (INFUSE framework)
- @.claude/skills/vapi-voice-ai/SKILL.md — VAPI voice agents (Assistants/Squads/Workflows)
- @.claude/skills/ultravox-voice-ai/SKILL.md — Ultravox voice agents (v0.7 GLM 4.6)
- @.claude/skills/chatbot-analytics/SKILL.md — AI conversation metrics and dashboards
- @.claude/skills/workflow-builder/SKILL.md — Repeatable business process mapping (cadence, milestones)
- @.claude/skills/workflow-decomposition/SKILL.md — Decompose ops into automation-ready workflows (NOW/SOON/LATER)
- @.claude/skills/ai-change-management/SKILL.md — ADKAR adapted for AI rollout
- @.claude/skills/ai-culture-architect/SKILL.md — AI-positive culture as observable behaviour
- @.claude/skills/prompt-creator/SKILL.md — Web AI chat prompts (ChatGPT/Claude/Gemini)
- @.claude/skills/prompt-discovery/SKILL.md — PROMPT Framework requirements gathering
- @.claude/skills/one-shot-plan/SKILL.md — Prompt planning for automation workflows
- @.claude/skills/one-shot-prompt/SKILL.md — Final automation prompts (Make/Zapier/n8n/LangChain)
- @.claude/skills/model-specific-optimiser/SKILL.md — Optimise prompts for GPT-5.4 / Gemini 3 / Claude 4.6
- @.claude/skills/skills-creator/SKILL.md — Author new SKILL.md files for Claude Code
- @.claude/skills/md-architect/SKILL.md — Architect/audit CLAUDE.md/GEMINI.md/AGENTS.md/MEMORY.md
- @.claude/skills/context-compress/SKILL.md — Compress always-loaded context files (40-50% token reduction)
- @.claude/skills/hormozi-offer/SKILL.md — Value Equation, Grand Slam Offers, guarantees
- @.claude/skills/hormozi-money-models/SKILL.md — Pricing, RAISE, Fast Cash, LTV levers, CFA
- @.claude/skills/hormozi-sales/SKILL.md — CLOSER, Onion of Blame, BAMFAM, nurture
- @.claude/skills/hormozi-marketing/SKILL.md — Core Four, More-Better-New, Lead Magnets/Getters
- @.claude/skills/hormozi-content/SKILL.md — Hooks, Ad Assembly, 5 Meats, Marketing Machine
- @.claude/skills/hormozi-retention/SKILL.md — Churn Checklist, 5 Horsemen, Activation Points
- @.claude/skills/hormozi-discovery/SKILL.md — 7-question business diagnosis and bottleneck routing
- @.claude/skills/image-generation-director/SKILL.md — AI image prompting (Nano Banana/DALL-E/MJ/Flux/Ideogram)
- @.claude/skills/video-generation-director/SKILL.md — Cinematic AI video prompting (Veo/Sora/Runway/Kling)
- @.claude/skills/ui-ux-pro-max/SKILL.md — UI/UX intelligence (styles, palettes, fonts, stacks)
- @.claude/skills/gdocs-sync-protocol/SKILL.md — Markdown ↔ Google Docs styling sync for playbooks
- @.claude/skills/competitive-ads-extractor/SKILL.md — Competitor ad library extraction
- @.claude/skills/docx/SKILL.md — Create/edit Word documents
- @.claude/skills/xlsx/SKILL.md — Create/edit/clean spreadsheets

## Quick Start (Gemini CLI / Antigravity)

1. Open Gemini CLI or Google Antigravity in this project directory.
2. Read `cos.yaml` for current TORQUE phase, gates, and constraint.
3. Load the orchestrator: `@.claude/agents/orchestrator.md`
4. Follow the orchestrator's guidance through each TORQUE phase.

## Core Operating Principles

### 1. COS-First Protocol
- Read `cos.yaml` before every decision — it contains phase status, gates, metrics, and client context.
- Update `cos.yaml` after every meaningful change via the `cos-update` skill (honest-confirm; never claim "saved" if not persisted).
- Check blocking gates before advancing a phase: tone of voice (PASSED), data access, baseline metrics validated.

### 2. Primary Constraint: Monetisation
Three businesses (FFG, FHL, UMI) operate in silos with no unified customer view or systematic cross-sell. Playbooks are delivered via GHL + integrations to Fox's existing providers (POLR custom platform paused per Apr 16 Mati decision).

### 3. Spawned Agent Sandbox
Subagent file writes do NOT persist. Extract deliverables from agent task output and write the files yourself.

### 4. Zero Fabrication in Client Comms
Every name, number, date, quote, decision, or commitment in client-facing artefacts must come from a verified source (cos.yaml, Fathom transcript, email thread, `/docs/`, or James in this session). If unsure → ask or leave blank. Never invent. See `CLAUDE.md` for full rule + verified stakeholder list.

### 5. Workbench Rule
Use `.tmp/` for intermediate files, scratch scripts, log outputs. Project root holds finalised deliverables only.

## Writing Standards

- **Language:** Australian English (colour, organise, behaviour, realise) — US spelling is auto-fail
- **Reading Level:** Third-grade for clarity (Flesch-Kincaid 80+)
- **Currency:** AUD ($) unless explicitly stated otherwise
- **Formatting:** No em dashes. No banned words (delve, leverage, navigate, robust, unlock, tapestry, etc.)
- **Voice:** Match `playbooks/master-playbook/tone-of-voice.md` exactly. StoryBrand framework (customer = hero, Fox = guide). Run `voice-humaniser` on AI-drafted content before it ships.
- **Compliance:** Never use "advice", "guarantee", or "financial hardship" in client-facing content.

---

*Generated by Njin Method Framework — entry point regenerated by the initialization agent on every deploy.*
