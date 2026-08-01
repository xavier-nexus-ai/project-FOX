# Framework Reference: OpenClaw Social Agent

## Purpose

A social-media-first AI assistant deployment for content creators, coaches, and agency owners. Turns a VPS into an AI-powered social media command centre — automated content creation, multi-platform publishing, blog automation, and a branded dashboard built on the AIpreneurs dark-theme design system.

## Target Audience

Content creators, online coaches, course creators, and digital agency owners who produce regular social content across multiple platforms and want AI to handle drafting, scheduling, publishing, and morning briefings — while they focus on strategy and final approval.

**Client signals that indicate fit:**

- Actively publishing to Instagram and/or YouTube
- Wants to scale content output without scaling time
- Needs a content pipeline (ideation → draft → review → publish)
- Running a blog alongside social and wants SEO/GEO-scored automation
- Wants Telegram as a mobile command interface for briefings and approvals
- Values a branded, premium-looking dashboard
- Open to AI-generated images and thumbnails via fal.ai
- Doesn't need a full general-purpose command centre — social and content is the focus

## Phases / Methodology

18 phases across 3 categories. Categories A and B are sequential. Category C modules are largely independent once the core is built.

**Category A — Foundation (Phases 1–6)**

| Phase | Name | What Gets Built |
|-------|------|-----------------|
| 1 | VPS Setup | Server provisioned, OpenClaw installed, safety net configured |
| 2 | Context Engineering | Workspace files: AI identity, content voice, audience profiles, platform tone |
| 3 | Config Tuning | Gateway config, model routing, content skills installed |
| 4 | Intelligence & Memory | Perplexity search connected, memory scaffolding set up |
| 5 | Telegram | Bot created, group set up, topic threads for content briefs and approvals |
| 6 | Social Integrations | Instagram and YouTube connected, fal.ai for media generation, OpenRouter for premium model access |

**Category B — Dashboard Core (Phases 7–14)**

Builds the AIpreneurs dark-theme Command Centre in Next.js:

| Phase | Name | What Gets Built |
|-------|------|-----------------|
| 7 | Architecture | Dashboard shell — full sidebar, all pages stubbed with "Coming Soon" overlays |
| 8 | Template Setup | Dashboard template configured with brand colours and AIpreneurs design system |
| 9 | Data Layer | API routes, data models, dashboard data pipeline |
| 10 | Cron Management | Cron page — job list with status badges, morning brief scheduling |
| 11 | Chat | Chat interface with topic sidebar |
| 12 | Goals & Tasks | Goal progress + Kanban task board |
| 13 | Approvals & Memory | Approvals queue + memory management interface |
| 14 | Activity & Search | Activity feed + search across content and briefs |

**Category C — Social Modules (Phases 15–16)**

| Phase | Name | What Gets Built |
|-------|------|-----------------|
| 15 | Content Studio & Publishing | Multi-platform publishing workspace — AI drafts, pipeline Kanban, calendar, ideas table, image and video studio |
| 16 | Blog Automation | SEO/GEO-scored blog pipeline with auto-publishing |

Category C phases can be selected independently. A client who only needs the content studio does not need to take blog automation.

Each phase follows: **Route → Build → Deploy → Validate → Complete → Next.** One phase at a time, always. Nothing auto-advances.

## Key Deliverables

- Production OpenClaw Social Agent running on a client-controlled VPS
- Telegram command centre with briefings, content summaries, and approval threads
- AIpreneurs dark-theme Next.js dashboard with:
  - Content Studio (drafts, pipeline Kanban, publishing calendar, ideas)
  - Video Studio and Image Studio
  - Chat, Briefs, Goals, Cron management, Approvals
- Instagram and YouTube publishing integrations
- AI media generation via fal.ai (thumbnails, social graphics, short video)
- Blog automation with SEO/GEO scoring and auto-publish
- Automated cron jobs: morning brief, evening summary, content scanning, social processing
- `project.json` — ongoing deployment state file

## Blocking Gates / Phase Dependencies

- **Category A (Phases 1–6) must complete in order before Dashboard Core can begin**
- Phase 7 (Dashboard Architecture) requires all of Category A
- Category B phases build on each other — each page phase requires the architecture and data layer phases before it
- Category C (Social Modules) requires core dashboard phases to be complete before activation
- Human validation is required at the end of every single phase — the orchestrator will refuse to mark a phase complete without explicit client confirmation that it is working on the VPS

## Key Agents

| Agent | Role |
|-------|------|
| `@orchestrator` (Conductor) | Persistent coordinator — tracks 18-phase progress by category (A/B/C), routes work, enforces dependencies, regenerates CLAUDE.md after each phase |
| `@init` (Scaffold) | One-time setup — scaffolds directories, copies agents to both Claude Code and Gemini formats |
| `@onboard` (Navigator) | Social-focused interview — platforms, content strategy, audience, tone, publishing cadence |
| `@prompt-engineer` (Wordsmith) | Generates workspace files with content voice, brand tone, and audience profiles |
| `@openclaw-specialist` (Gateway) | Social cron jobs, content skills, gateway config, model routing |
| `@frontend-developer` (Builder) | Builds the AIpreneurs dark-theme Command Centre and all dashboard pages |
| `@deployer` (Deployer) | Safe VPS deployment with rollback — the only agent that touches production |
| `@integration-specialist` (Connector) | Telegram, Instagram, YouTube, Perplexity, fal.ai, and OpenRouter setup |

## Typical Engagement Shape

**Duration:** 6–12 weeks. Foundation through full Dashboard Core (Phases 1–14) is typically 5–8 weeks. Social modules add 1–2 weeks each.

**Technical requirements:**

- VPS: Ubuntu 22+ with 2GB+ RAM
- Claude Code installed on client's local machine (or Gemini CLI)
- Anthropic API key or Claude Pro/Max subscription
- Telegram account for bot creation
- Instagram Business or Creator account
- YouTube channel with a Google Cloud project (for YouTube Data API)
- fal.ai account for AI media generation (optional but recommended)
- OpenRouter account for premium model access (optional)
- Perplexity API key for social intelligence search

**Team involved:** One technical consultant running sessions with the client. Client participates in onboarding, validates each phase, and approves content going live. No developer required.

## How to Scope This Framework

1. **Confirm the platforms.** Instagram and YouTube are the primary publishing targets. If the client is only on LinkedIn or X, this framework is not the right fit — those platforms are not in the integration stack.
2. **Category A and B are the base.** Always include Phases 1–14 in full. This is the foundation and dashboard. Category C is add-on.
3. **Content Studio (Phase 15) is the main differentiator.** Almost every social-focused client will want this. Blog Automation (Phase 16) is optional and adds scope.
4. **fal.ai is optional but high-value.** Clients who produce visual content (thumbnails, graphics, clips) should be encouraged to include it — it's configured in Phase 6.
5. **Budget 2–4 hours per phase** including build, test, VPS deploy, and client validation.
6. **Onboarding is social-focused.** The `@onboard` wizard collects platforms, content cadence, audience profiles, brand tone, and publishing preferences. Allow 1–2 hours for the first session.
7. **Design system is fixed.** The dashboard uses the AIpreneurs dark theme (black background, red/coral brand accent, glassmorphism cards). Clients who need a different visual identity need a custom build, not this framework.

## Signals This is the Right Framework

- Content creator, coach, or agency owner publishing regularly to Instagram and/or YouTube
- Wants to automate content drafting, scheduling, and publishing without losing control of final approval
- Needs a visual content pipeline they can review on a dashboard
- Wants Telegram as a mobile briefing and approval interface
- Running a blog alongside social and wants SEO automation
- Comfortable with AI-generated image and video assets
- Values a premium dark-theme dashboard aesthetic
- Has or will get a VPS and is willing to own their infrastructure

## Signals This is NOT the Right Framework

- Client primarily publishes to LinkedIn or X — integrations don't cover these platforms
- Needs a full general-purpose AI command centre beyond social and content (use OpenClaw Orchestrator instead)
- No Telegram — unwilling to adopt it as a mobile interface
- Wants a pure SaaS tool with no server management — this requires a VPS the client controls
- Needs heavy team collaboration features or multi-user access
- Short timeline and only wants one or two features — this is a full system build

## Source Materials

- `/docs/background/frameworks/openclaw-social-agent/README.md`
- `/docs/background/frameworks/openclaw-social-agent/CLAUDE.md`
- `/docs/background/frameworks/openclaw-social-agent/agents/orchestrator.md`
- `/docs/background/frameworks/openclaw-social-agent/agents/onboard.md`
