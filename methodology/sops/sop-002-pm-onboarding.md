# SOP-002: PM Onboarding — New Project Manager

## Title and Purpose

**Title:** PM Onboarding SOP — New Project Manager Setup
**Purpose:** Get a new PM (George, Michael, or future hire) fully operational with the Njin PM Framework. Covers tool setup, framework comprehension, a practice run, and GitHub workflow. PM should be able to run a full init/discovery/scope cycle independently after completing this SOP.

---

## Trigger

A new PM joins the Njin team, OR an existing PM is granted access to the PM Framework for the first time.

---

## Prerequisites

- PM has been briefed on the Njin business model and active clients
- PM has a MacOS laptop (Claude Code runs locally)
- PM has a GitHub account to be added to the `engine-pm` org
- James or George is available to supervise the practice run (Step 5)

---

## Steps

### Step 1 — Install Claude Code

**Who:** New PM (with help from Xavier if needed)
**What:**
1. Install Claude Code from `claude.ai/code` — follow the official install instructions
2. Verify Claude Code launches and the PM can open a project folder
3. Confirm the PM understands the difference between a normal conversation and **plan mode** — plan mode must be used before executing any significant action. To activate: type `/plan` before describing a task, or enable in Claude Code settings.

**Output:** Claude Code installed and working. PM understands plan mode.

---

### Step 2 — Understand the Framework Structure

**Who:** New PM
**What:**
Read the following files in order — do not skip:

| File | What it tells you |
|---|---|
| `CLAUDE.md` | The operating map — agents, skills, workflow, key rules |
| `cos.yaml` | The state file — what phase the project is in, what's done, what's blocked |
| `.claude/agents/orchestrator.md` | The central entry point — this is how you open every session |
| `.claude/agents/initialization-agent.md` | One-time setup agent — runs when a new client project starts |
| `.claude/agents/business-analyst.md` | Discovery and scoping agent |
| `.claude/agents/coordinator.md` | Sprint planning and estimation agent |
| `.claude/agents/communication-agent.md` | Client-facing output agent |

Key concepts to understand before moving on:

- **The Orchestrator is the PM** — it is the central entry point, not a supervisory layer sitting above the PM
- **COS is the state file** — it tracks where the project is across sessions. Read it before every session.
- **Handoff documents** connect agents — each agent produces a handoff document. The PM reviews it before passing work to the next agent.
- **Plan mode is mandatory** for anything significant — always plan before executing
- **Spawned agents are sandboxed** — file writes from subagents do not persist. The PM (parent session) must write files after reviewing agent output.

**Output:** PM can describe the framework structure and purpose of each agent without referring to notes.

---

### Step 3 — Deploy to a Test Project

**Who:** New PM (supervised by James or Xavier)
**What:**
1. Create a folder called `test-client/` in a safe working directory (not a live client folder)
2. Run the deploy script: `scripts/deploy.sh test-client`
3. Verify the following are present in `test-client/`:
   - `.claude/agents/` — all agents present
   - `.claude/skills/` — all skills present
   - `cos.yaml` — blank template
   - `CLAUDE.md` — client-specific config template
4. Open Claude Code in `test-client/` and load the Orchestrator: `@.claude/agents/orchestrator.md`
5. Confirm agents load without errors

**Output:** Test project deployed. PM has run a deploy from scratch and confirmed it works.

---

### Step 4 — Run a Practice Init/Discovery/Scope Cycle

**Who:** New PM (supervised by James or George)
**What:**

Use a sample client brief (James to provide a redacted example from an existing client — e.g. a simplified Avanti or Dexion brief).

1. **Init:** Load Orchestrator > run Initialisation Agent > feed it the sample brief > review the populated `cos.yaml`
2. **Discovery:** Load Business Analyst > run Discovery Skill > review the document plan it produces > compare against what's provided > review its gap analysis
3. **Scope:** After discovery is marked complete in `cos.yaml`, run Scoping Skill > review the scope document produced
4. At each agent handoff, PM reviews the handoff document before proceeding — do not auto-advance
5. After the full cycle, PM and supervisor debrief: what went well, what was confusing, what needed correction

**Key checkpoint:** Michael's Avanti project plan was flagged as incorrect because it was created from the proposal alone, without consulting the framework delivery procedure. This practice run specifically trains the PM to follow the framework-aligned process, not shortcut it.

**Output:** PM has completed a full init/discovery/scope cycle on a test project. Debrief notes recorded.

---

### Step 5 — Understand the GitHub Workflow

**Who:** New PM (with Xavier)
**What:**
1. Xavier adds the PM to the `engine-pm` GitHub org
2. PM clones the relevant repo for their first live client project
3. PM understands the commit and push cadence: **weekly minimum**, more frequently when significant changes occur
4. PM understands the conflict rule: **two people cannot work on the same framework files simultaneously** — coordinate with James or George before opening a client project folder
5. PM confirms they can: clone a repo, make changes, commit, and push without assistance

**Output:** PM added to `engine-pm` org. PM can commit and push independently.

---

### Step 6 — Learn the njin-vibe Sync Skill

**Who:** New PM
**What:**
1. Read the `njin-vibe-sync` skill file in `.claude/skills/`
2. Understand that njin-vibe sync is a **skill, not an agent** — it is called from the Coordinator, not as a standalone session
3. Understand when sync is triggered (agreed checkpoints — confirm with James which checkpoints apply)
4. PM does not need to operate the sync manually until the first live client project

**Output:** PM understands njin-vibe sync conceptually. Ready for first live use.

---

### Step 7 — Weekly Training Sessions

**Who:** New PM + James + George + Xavier
**What:**
- Attend weekly AI training session (5pm, day TBC — confirm with James)
- Sessions cover: new framework features, edge cases encountered that week, Q&A
- PM raises any confusion from practice run or live work during these sessions

**Output:** PM enrolled in weekly training sessions.

---

## Quality Check

Before the PM is cleared to run a live client project independently:

- [ ] Claude Code installed and working
- [ ] PM can describe all agents and their roles from memory
- [ ] PM has deployed a test project from scratch
- [ ] PM has completed a full init/discovery/scope cycle on a test project
- [ ] Debrief completed with James or George — no unresolved confusion
- [ ] PM added to `engine-pm` GitHub org and can commit/push independently
- [ ] PM understands plan mode and uses it before executing
- [ ] PM understands the spawned agent sandbox constraint (no file writes persist from subagents)
- [ ] PM enrolled in weekly training sessions

---

## Output

- PM cleared to run live client projects independently
- Test project folder retained as reference material
- Debrief notes filed in PM training records
