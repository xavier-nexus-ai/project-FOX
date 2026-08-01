# Framework Reference: OpenClaw Orchestrator

## Purpose

A phased deployment framework for building a fully customised AI assistant command centre — personal or business-wide — with Telegram integration, a Next.js dashboard, VPS-hosted automation, and external service connections. Gives the client a "done with them" path to a production AI system they own and operate themselves.

## Target Audience

Founders, executives, consultants, and operators who want a private, self-hosted AI chief of staff or command centre. Usually running multiple businesses or roles and needing to centralise decisions, communications, content, and automation in one place.

**Client signals that indicate fit:**

- Wants a personal AI assistant with its own identity (name, personality, tone)
- Already using or open to Telegram as a mobile command interface
- Has or is willing to set up a VPS (cloud server)
- Needs to consolidate tasks, briefs, approvals, and communications into one tool
- Wants proactive AI — morning briefs, evening summaries, automated workflows
- Interested in LinkedIn intelligence, lead gen, content creation, or analytics via AI
- Running multiple businesses that each need separate context but one AI instance

## Phases / Methodology

The framework has 35 phases across 5 categories. Foundation (Category A) is mandatory and sequential. All other categories are pick-and-choose based on client need. The orchestrator enforces the dependency graph — no phase can start until its prerequisites are confirmed working.

**Category A — Foundation (Phases 1–7)**

| Phase | Name | What Gets Built |
|-------|------|-----------------|
| 1 | VPS Setup | Server provisioned, OpenClaw installed, SSH configured |
| 2 | Context Engineering | Workspace files: SOUL.md, IDENTITY.md, USER.md, GOALS.md, PLAYBOOK.md, etc. |
| 3 | Telegram | Bot created, group set up, topic threads organised |
| 4 | Integrations | Core external services connected (Google, Outlook, Slack, etc.) |
| 5 | Cron Automation | Morning briefs, evening summaries, heartbeat jobs scheduled |
| 6 | Gateway Config | OpenClaw config, model routing, CLI commands |
| 7 | Phase 7 | (Dependent on selected features — finalises foundation) |

**Category B — Dashboard Core (Phases 8–19)**

Builds the Next.js Command Centre: overview stats, goals/tasks, chat interface, approvals queue, memory management, briefs, projects. Progressive deployment — each page activates as its phase completes.

**Category C — Extended Core (Phases 20–24)**

Documents, contacts, MCP server management, skills library, models configuration.

**Category D — Domain Modules (Phases 25–33)**

Pick-and-choose capability layers: Email, LinkedIn Intelligence, Lead Gen, Content Studio, Blog, Video, Skool community integration, Accountability, Analytics.

**Category E — Strategy & Media (Phases 34–35)**

Vector DB and semantic search (RAG context), Image Studio with AI media generation.

Each phase follows the same lifecycle: **Route → Build → Local Test → Deploy Plan → VPS Deploy → Validate → Complete → Next.** Nothing goes live until the client explicitly validates it.

## Key Deliverables

- Production OpenClaw instance running on a VPS the client controls
- Telegram command centre with organised topic threads and automated briefings
- Next.js dashboard (Command Centre) accessible via browser — branded to the client
- Workspace files defining the AI's identity, personality, goals, and knowledge base
- Automated cron jobs for briefs, summaries, and content scanning
- External integrations (Google, Outlook, Slack, and domain-specific services)
- Domain modules as selected (LinkedIn, lead gen, content, blog, video, analytics, etc.)
- `project.json` — ongoing state file tracking all deployment decisions

## Blocking Gates / Phase Dependencies

- **Category A must complete in full before Dashboard or Domain phases begin**
- Phase 8 (Dashboard Architecture) requires Phases 1–7
- Extended Core (Phases 20–24) requires full Dashboard Core (through Phase 19)
- Domain Modules (Phases 25–33) all require Phase 19 (full core deployed)
- Phase 35 (Image Studio) requires Phase 28 (Content Studio)
- Phase 36 (Agent Team Design — optional) requires Phase 3 and multi-agent mode selected at onboarding
- Human validation is required after every single phase before the next can begin — the orchestrator will refuse to advance without explicit client confirmation

## Key Agents

| Agent | Role |
|-------|------|
| `@orchestrator` (Conductor) | Persistent coordinator — tracks state, routes work, enforces dependencies, regenerates CLAUDE.md after each phase |
| `@init` (Scaffold) | One-time setup — creates directories, copies agents, generates initial files |
| `@onboard` (Navigator) | Interactive wizard — collects client info, branding, infrastructure details, and feature selections |
| `@prompt-engineer` (Wordsmith) | Generates workspace files (SOUL.md, IDENTITY.md, USER.md, etc.), system prompts, and AI personality |
| `@openclaw-specialist` (Gateway) | Configures OpenClaw gateway, CLI, cron jobs, model routing, and skills |
| `@frontend-developer` (Builder) | Builds and extends the Next.js Command Centre |
| `@deployer` (Deployer) | Handles all VPS operations — the only agent that touches production |
| `@integration-specialist` (Connector) | Sets up external services — Telegram, Google, Slack, Outlook, OAuth flows |

## Typical Engagement Shape

**Duration:** 8–16 weeks depending on phase selection. Foundation through full Dashboard Core is typically 6–10 weeks. Domain modules add 1–2 weeks each.

**Technical requirements:**

- VPS: Ubuntu 22+ with 2GB+ RAM (client sources this; Digital Ocean, Hetzner, or similar)
- Node.js 18+ on the VPS
- Claude Code or Gemini CLI installed on the client's local machine
- Anthropic API key or Claude Pro/Max subscription
- Telegram account for bot creation
- External service accounts as required per selected modules (Google, Outlook, LinkedIn, etc.)

**Team involved:** One technical consultant running sessions with the client. The client participates in onboarding, validates each phase, and approves deployments. No developer required unless Domain modules need custom integrations.

## How to Scope This Framework

1. **Start with feature selection.** The 35 phases are optional beyond Category A. Identify which Domain modules the client actually needs — don't quote all 35.
2. **Confirm VPS access.** If the client doesn't have one, factor in procurement and setup time. First session is often just VPS setup and SSH access.
3. **Count phases, not weeks.** Each phase is one validated deployment. Budget roughly 2–4 hours per phase including build, local test, VPS deploy, and client validation.
4. **Onboarding is non-trivial.** The `@onboard` wizard collects AI name, tone, business context, branding, and infrastructure details. This shapes everything downstream. Allow 1–2 hours for the first session.
5. **Dashboard Core is a significant chunk.** Phases 8–19 are 12 pages of Next.js. Budget accordingly. If the client doesn't need a dashboard, scope Category A only.
6. **Category C and D are modular.** Each domain module (LinkedIn, Lead Gen, Blog, etc.) can be scoped and added later. Good for phased billing.

## Signals This is the Right Framework

- Client wants a self-hosted, privately owned AI system — not a SaaS subscription
- Actively using Telegram or willing to adopt it as their command interface
- Running complex operations across multiple businesses or teams
- Wants proactive AI (briefings, summaries, automation) not just chat
- Has the technical appetite to manage a VPS (or has someone who can)
- Interested in multiple domain modules — LinkedIn, content, lead gen, analytics
- Budget and timeline support a multi-week build engagement

## Signals This is NOT the Right Framework

- Client wants a quick win or a simple chatbot — this is infrastructure, not a widget
- No VPS, no technical resource, and unwilling to learn basic server management
- Purely social-media-focused without other command centre needs (use Social Agent instead)
- Client needs a team-facing tool rather than a personal AI command centre
- Timeline is under 4 weeks and they want everything working now

## Source Materials

- `/docs/background/frameworks/openclaw-orchestrator/README.md`
- `/docs/background/frameworks/openclaw-orchestrator/CLAUDE.md`
- `/docs/background/frameworks/openclaw-orchestrator/agents/orchestrator.md`
- `/docs/background/frameworks/openclaw-orchestrator/agents/onboard.md`
