# MASTER PLAN: Customer Use-Case AI Application

> **This file is the single source of truth for the project.**
> Every prompt, idea, change, decision and fix goes through it, whatever AI model, tool, chat or person is working.
> If anything else (a chat, a doc, code, memory) disagrees with this file, **this file wins** until it's updated.

| | |
|---|---|
| **Version** | v8.2 (Claude Code in VS Code builds the kit itself from this plan + `VSCODE_HANDOFF.md`) |
| **Last updated** | 14 Oct 2026 |
| **Owner** | Patrick (Lead and builder) |
| **Canonical location** | Project doc `MASTER_PLAN.md` (planning chat) **and** `docs/MASTER_PLAN.md` in the local repo (builder). The local repo copy wins during the build; it's uploaded back to the Project at the end of the day |

---

## ⭐ RULE ZERO: ALWAYS INTERACTIVE (the most important rule in this file)

> **The Assistant never decides alone. It stays connected with Patrick and asks before moving on.**

1. **Ask, don't assume.** Whenever the Assistant finds a **gap** (in the use case, requirements, data, design, architecture or tests), **needs a detail**, or faces **any choice**, it **stops and asks**.
2. **Offer options.** 2–4 clear options per question, **recommended option first** with a one-line reason; Patrick can confirm in one click or type his own answer.
3. **Confirm before proceeding.** No step is started, no decision logged and no option chosen until Patrick confirms. Confirmed answers go straight into the Decisions log (9.1).
4. **Ask early, batch smartly.** Up to 4 questions at a time, as soon as a gap appears; work that doesn't depend on the answer continues meanwhile.
5. **Report back after every step:** what was done, docs updated, next step, **questions needing Patrick's answer**.
6. **If Patrick isn't available:** prepare the options and reversible groundwork, then **wait**. Never pick on his behalf.
7. **No question needed** to carry out an already-confirmed decision. Commands, installs, builds and tests run without asking (Rule 1); **deleting anything always needs approval** (Rule 2).

This applies equally to **Claude Code in VS Code** (the builder): its `CLAUDE.md` tells it to follow Rule Zero.

---

**Contents:** 1 How this file is used · 2 Snapshot · 3 Rules · 4 Models and stack · 5 Today's timeline and tracker · 6 Steps · 7 AI library · 8 Design system · 9 Logs and risks · 10 Changes and new ideas · 11 Testing · 12 Test and demo data · 13 Winning the customer's confidence · 14 Scope: kept, right-sized, deferred · 15 Readiness confirmation

---

## PART 1: HOW THIS FILE IS USED

### 1.1 Two Claude roles, one plan
| Role | Where | Does |
|---|---|---|
| **Planner (the Assistant)** | This claude.ai Project chat | Analyses the use case, asks questions, writes and updates the docs, generates the ideas, writes the build prompts, reviews results |
| **Builder** | **Claude Code in VS Code** on Patrick's Windows laptop (WSL2) | Builds, runs and tests the app locally from `docs/` and `docs/BUILD_PROMPTS.md`, following `CLAUDE.md` |

Patrick moves between them: the Planner's files go into the repo; the Builder's results (test output, screenshots, questions) come back to the Planner when a decision or a doc update is needed.
**Usage tip (Pro plan):** both share one usage allowance, so keep the planning chat focused during the build (R4).

### 1.2 The prompt protocol: every request follows these 6 steps
1. **Read** this file first: Rule Zero, Part 2 (snapshot), Part 3 (rules), and the step or section the request touches.
2. **Locate** the request: which Step (Part 6) or Section? If none, it's a **change** (Part 10).
3. **Check** against Rule Zero, the Rules and the Decisions log. If anything conflicts, is missing, or has options, **ask Patrick with options**.
4. **Do** the work, following the step's "Does" and "Done when".
5. **Update** in the same turn: Part 2 snapshot, Part 5 tracker, Part 9 logs, and every affected doc (10.2).
6. **Reply** with: what was done, **"Docs updated"**, the next step, and **the open questions for Patrick**.

### 1.3 Where this plan is wired in
| Place | What it says |
|---|---|
| Project instructions (claude.ai) | "Before answering any prompt, read MASTER_PLAN.md and follow Rule Zero and Part 1." |
| Repo `CLAUDE.md` (Claude Code) | Read `docs/MASTER_PLAN.md` first; follow Rule Zero; follow the Definition of Done (10.3); run `make check` before saying a task is done |
| Project memory | This file governs all work; Rule Zero |
| `make check` | Runs the tests, data checks and the docs guard locally, which is the gate for every change (Part 11) |

---

## PART 2: PROJECT SNAPSHOT (update on every change)

| Item | Current value |
|---|---|
| Goal | Build a **small, polished, working AI application for one customer use case** (dashboard + AI agents) **today**, run it locally in containers, and demo it tomorrow so convincingly that the customer is confident to invest (Part 13) |
| Timeline | Use case arrives **this afternoon (14 Oct)** → **~3.5 h** to complete everything today → **demo tomorrow (15 Oct) morning**; no work possible tomorrow |
| Team | **Patrick + Claude Code** (one build lane) + this Planner chat as a second lane |
| Machine | **Windows laptop**: WSL2 (Ubuntu) + Docker Desktop + VS Code + Claude Code extension |
| Run mode | **Local only**: Docker Compose containers on localhost ports; no GitHub, no cloud deploy |
| AI models | **Not known yet**: Patrick provides the available models and keys at the lab; the app is model-agnostic (4.1) |
| Use case | **Not received yet** (arrives this afternoon) |
| AI ideas | **5 hero candidates + 5 supporting candidates → Patrick picks 2 hero + 2 supporting** |
| Product name | Not chosen (8.4) |
| Current step | **Phase A: A2.** Claude Code (VS Code, logged in) builds the kit from `docs/MASTER_PLAN.md` + `docs/VSCODE_HANDOFF.md` (D23) |
| Next action | Patrick puts both files in `~/projects/app/docs/` and pastes the kick-off message → Claude Code checks tools (A1) and builds the kit (A2) → use case → Step 1 |
| Open questions | 9.3 |

---

## PART 3: RULES

1. **Run commands without asking.** Installs, scaffolding, builds, tests, local git commits, containers.
2. **Ask before deleting, every time.** Files, folders, containers with data, volumes, databases, Project docs.
3. **Search the internet freely** for docs, versions, examples and fixes.
4. **Latest versions, then freeze.** Install the latest at setup; lockfiles; record the versions in `ARCHITECTURE.md`; no upgrades after the build starts unless something is broken.
5. **Models are configuration.** Model names and keys live only in `.env`; roles (planner / worker / fast / embeddings) are mapped once the available models are known (Step 2).
6. **Plan before feature code.** No feature code until the **gate (Step 8)**; the use-case-independent skeleton may be built earlier.
7. **Living docs.** Every agreed change updates its doc(s) in the same step (10.2) and meets the Definition of Done (10.3).
8. **Final docs come last** (Step 13), but working docs are always current.
9. **Right-sized.** It's a single use case: build what proves value; defer the rest to the roadmap (Part 14).
10. **One working flow beats five broken ones.** Feature freeze at Step 11.
11. **Design rules are fixed** (Part 8): glassmorphism + bento, **no dark blue / navy**, icon-only sidebar, clean headers (logo + name + page heading only), unique name and logo.
12. **AI safety rules** (7.3): read-only by default, role-aware, hard DB limits, approval before any write or send, sources on every answer, structured outputs.
13. **Data privacy.** No real customer data without consent; default synthetic data (Part 12).
14. **Time box.** The Planner reports time used vs budget (5.1) at each checkpoint and proposes cuts if needed; **cuts are confirmed by Patrick** (Rule Zero).
15. **Honest scope.** Integrations labelled *Real / Sandbox / Mocked*; the app is presented as a working prototype on real architecture.
16. **Tests from the first prompt.** Every build prompt ends with tests and `make check` (Part 11).
17. **Test data is managed.** Generated, deterministic, validated and story-driven, never hand-typed (Part 12).
18. **Windows/WSL hygiene.** The repo lives inside the WSL filesystem (e.g. `~/projects/app`), not on `C:\`; containers run through Docker Desktop's WSL integration.
19. **Keys stay in `.env`.** Never commit them or export them globally in the shell (an exported `ANTHROPIC_API_KEY` would make Claude Code bill that key instead of the Pro subscription).

---

## PART 4: MODELS AND STACK

### 4.1 AI models: model-agnostic by design
The available models are provided at the lab. The app talks to models through **LangChain's provider-neutral chat model interface** (`init_chat_model`), so any of these work with a config change: **Azure OpenAI / AI Foundry, AWS Bedrock (incl. Claude), Google Vertex / Gemini, OpenAI, Anthropic API**.

| Role | Used for | Pick from the available models | `.env` key |
|---|---|---|---|
| **Planner** | Multi-step reasoning, the orchestrator's plan | The strongest model available | `MODEL_PLANNER=provider:model` |
| **Worker** | Most agent work: Q&A, insights, drafting | A strong, fast mid-tier model with reliable tool calling | `MODEL_WORKER=provider:model` |
| **Fast** | Routing, classification, extraction, verification | The cheapest fast model | `MODEL_FAST=provider:model` |
| **Embeddings** | Document search, similar records (only if an idea needs it) | Any embeddings model available (e.g. Azure `text-embedding-3-*`, Bedrock Titan/Cohere, Vertex, Voyage) | `MODEL_EMBED=provider:model` |
| **Speech** (only if a voice idea is chosen) | Speech-to-text / text-to-speech | The provider's speech service, or Sarvam for Tamil/Hindi | `SPEECH_PROVIDER=…` |

**Model check at Step 2 (10 min):** `make models-check` calls each configured model and checks (1) tool calling, (2) valid JSON for a schema, (3) first-token latency under 3 s. The Planner proposes the role mapping from the results, and **Patrick confirms it** (Rule Zero).
**Cost controls:** fast model for routing; capped `max_tokens` per agent; per-user rate limit; token usage logged in the audit trail.

### 4.2 Stack (local containers)
| Layer | Choice | Notes |
|---|---|---|
| Host | **Windows + WSL2 (Ubuntu) + Docker Desktop** (WSL integration on) | Repo inside WSL |
| Builder | **VS Code + WSL extension + Claude Code extension** (Pro login) | Opens the repo in WSL |
| Containers | **Docker Compose**: `db` (PostgreSQL + pgvector, :5432), `api` (FastAPI, :8000), `web` (Next.js, :3000), `mailpit` (:8025, only if an email action is chosen) | Health checks on every service; named volume for data |
| Backend | **Python (latest stable that installs cleanly)**, FastAPI, Pydantic, SQLAlchemy, Alembic, **uv** | API docs auto-generated at `/docs` |
| Auth | Simple JWT login (httpOnly cookie) with **2–3 demo personas/roles** | Roles enforced in the API and agent tools |
| Database | **PostgreSQL + pgvector** | **Read-only DB user for agents**; row limit + statement timeout |
| API types | TypeScript types generated from FastAPI's `/openapi.json` | Frontend and backend stay in sync |
| Frontend | **Next.js (latest)** + Tailwind + shadcn/ui (restyled to Part 8) + Recharts + Phosphor Icons | Glass + bento design system |
| Agents | **LangGraph** + provider-neutral chat models (4.1) + tools; **Postgres checkpointer** for chat threads and pending approvals | Human-in-the-loop approvals |
| Streaming | **Server-Sent Events** with events: `token`, `tool_call`, `source`, `approval_request`, `error`, `done` | |
| Observability | **Built-in AI audit trail** (table + UI panel: steps, tools, data touched, tokens, time) + structured JSON logs | Langfuse/Sentry deferred (Part 14) |
| Tests | pytest + httpx, vitest, **Playwright** (+ axe accessibility check), eval harness, attack prompts | One command: `make check` |
| Test data | `scripts/datagen/` with Faker (`en_IN`) + YAML config + validation checks | Part 12 |
| Quality gate | **`make check`**: ruff, eslint, typecheck, unit/API tests, data checks, eval smoke, Playwright smoke, docs guard, secret scan (gitleaks) | Replaces cloud CI |
| Version control | **Local git**: a commit per build prompt, a tag per milestone (`v0.1-skeleton`, `v1.0-demo`) | Rollback = checkout the tag + `docker compose up --build` |

---

## PART 5: TODAY'S TIMELINE AND TRACKER

### 5.1 Time budget (from the moment the use case arrives = T+0)
| Block | Steps | Planner (this chat) | Builder (Claude Code) | Budget | Checkpoint |
|---|---|---|---|---|---|
| **Before the use case** | A1–A3 | Build kit: docs, prompts, CLAUDE.md, templates | Patrick installs tools (A1) | Now → afternoon | Kit downloaded; tools installed |
| **Kick-off** | 1–2 | Use-case intake + questions | **Skeleton build starts in parallel** (BP-01 → BP-03) | T+0 → T+20 | Questions answered; models mapped |
| **Ideas** | 3–4 | 5 hero + 5 supporting ideas | Skeleton continues | T+20 → T+35 | **2 hero + 2 supporting picked** |
| **Plan docs** | 5–7 | PRD, data, architecture, agents, design, tests, data story, tailored build prompts | Skeleton finishes; `make check` green | T+35 → T+60 | Docs v1 |
| **Gate** | 8 | Gate checklist | — | T+60 → T+65 | **"Go" from Patrick** |
| **Build** | 9–10 | Answers builder questions; keeps docs in sync | Data → API → screens → hero 1 → hero 2 → supporting 1 → supporting 2 | T+65 → T+165 (100 min) | Hero 1 working by T+110 |
| **Freeze + test** | 11–12 | UAT checklist; triage | `make check-full`; fixes only | T+165 → T+190 | All green |
| **Final** | 13–14 | Final docs pack, investment pack, demo script | Tag `v1.0-demo`; backup video | T+190 → T+210 | Demo-ready (~3.5 h) |

**Cut order if behind schedule (confirmed by Patrick before cutting):** supporting idea 2 → supporting idea 1 → polish on secondary screens. **The two hero ideas are cut last.**

### 5.2 Tracker
| # | Step | Owner | Budget | Time | Status |
|---|---|---|---|---|---|
| A1 | Install tools on the laptop | Patrick | before | | ☐ |
| A2 | Build kit (docs + prompts) **by Claude Code in VS Code** from the handoff | Builder | ~15 min at the lab | | ☐ |
| A3 | Repo created from the kit; Claude Code reads `CLAUDE.md` | Patrick | before | | ☐ |
| 1 | Use-case intake + questions | Planner + Patrick | 15 min | | ☐ |
| 2 | Model check + role mapping | Builder + Patrick | 10 min ∥ | | ☐ |
| 3 | 5 hero + 5 supporting ideas | Planner | 10 min | | ☐ |
| 4 | Pick 2 hero + 2 supporting | Patrick | 5 min | | ☐ |
| 5 | PRD + data model + data story | Planner | 10 min | | ☐ |
| 6 | Architecture + agents + security + tests | Planner | 10 min | | ☐ |
| 7 | Design applied + tailored build prompts | Planner | 5 min | | ☐ |
| ∥ | Skeleton: environment, containers, auth, shell, test harness (BP-01 → BP-03) | Builder | T+0 → T+60 | | ☐ |
| 8 | **Gate** | Patrick | 5 min | | ☐ |
| 9 | Data + API + screens (BP-04 → BP-06) | Builder | 45 min | | ☐ |
| 10 | Hero 1, hero 2, supporting 1, supporting 2 (BP-07 → BP-10) | Builder | 55 min | | ☐ |
| 11 | **Feature freeze** | Patrick | — | | ☐ |
| 12 | Full test run + UAT + fixes (BP-11) | Builder + Patrick | 25 min | | ☐ |
| 13 | Final docs + investment pack | Planner | 10 min ∥ | | ☐ |
| 14 | Demo script, rehearsal, backup video, tag (BP-12) | Patrick | 15 min | | ☐ |

---

## PART 6: THE STEPS

### PHASE A: BEFORE THE USE CASE ARRIVES

#### A1: Install tools on the Windows laptop (Patrick, ~30–40 min, one-time)
1. **WSL2 + Ubuntu:** in PowerShell (as admin) `wsl --install -d Ubuntu`, reboot, create the Linux user.
2. **Docker Desktop:** install; Settings → Resources → WSL integration → enable for Ubuntu.
3. **VS Code:** install the **WSL** and **Claude Code** extensions; sign in to Claude Code with the Pro account.
4. **Inside Ubuntu (WSL):** `sudo apt update && sudo apt install -y git make build-essential curl`; install **uv** (`curl -LsSf https://astral.sh/uv/install.sh | sh`); install **Node LTS** via nvm.
5. Check: `docker run hello-world` works from Ubuntu.

**Done when:** `docker`, `git`, `make`, `uv`, `node` all respond inside WSL, and Claude Code opens in VS Code connected to WSL.

#### A2: Build kit (Builder = Claude Code in VS Code, from `docs/VSCODE_HANDOFF.md`; ~15 min)
`customer-app-kit.zip` contains:
- `CLAUDE.md` (builder rules)
- `docs/MASTER_PLAN.md`
- `docs/BUILD_PROMPTS.md` (BP-01 → BP-12, each with acceptance checks)
- the 8 working docs, pre-filled with everything that doesn't depend on the use case
- `docs/USE_CASE_INTAKE.md`
- the `docs/DEMO_DATA.md` template

#### A3: Create the repo (Patrick, 5 min)
1. In Ubuntu: `mkdir -p ~/projects && cd ~/projects`.
2. Unzip the kit there as `app/`, then `cd app && git init && git add . && git commit -m "kit"`.
3. `code .` to open it in VS Code (WSL).

**Done when:** Claude Code in VS Code confirms it has read `CLAUDE.md` and `docs/MASTER_PLAN.md`.

### PHASE B: KICK-OFF AND IDEAS (when the use case arrives)

#### Step 1: Use-case intake (Planner + Patrick, 15 min)
**Patrick:** pastes or uploads the use case into this chat **and** tells Claude Code to start **BP-01 → BP-03** (the skeleton doesn't depend on the use case).
**Planner:**
- runs the adapter playbook (7.4) and fills `USE_CASE_INTAKE.md`
- lists **every gap** as questions with options (Rule Zero): users and roles, top pains, KPIs, data available, which actions need approval, success criteria, branding, languages, integrations (Real/Sandbox/Mocked), data consent
- marks assumptions for anything nobody can answer

**Done when:** every question is answered or has a confirmed assumption (logged in 9.1).

#### Step 2: Model check and role mapping (Builder + Patrick, 10 min, in parallel)
**Patrick:** puts the available model names and keys into `.env` (never committed).
**Builder:** runs `make models-check` (built in BP-02).
**Planner:** proposes the Planner / Worker / Fast / Embeddings mapping. **Patrick confirms it**; the mapping is recorded in `ARCHITECTURE.md` and 9.1.

#### Step 3: 5 hero + 5 supporting ideas (Planner, 10 min)
**Planner:** writes **5 hero candidates** and **5 supporting candidates**, tailored to the use case (from the libraries in 7.1–7.2). Each idea gets:
- pitch and wow moment
- the agents involved and the data needed
- effort (S/M/L) within today's budget
- business value in the customer's own numbers
- demo risk

Ideas are ranked by **value × wow × feasibility ÷ effort**.
**Hero criteria:** hits a top pain · runs on their data shape · end-to-end (insight → recommendation → approved action) · measurable outcome · buildable today.
**Supporting criteria:** small (S), visibly useful, reuses the hero's agents or data.

#### Step 4: Pick 2 hero + 2 supporting (Patrick, 5 min)
**Planner:** asks, with the top 2 of each pre-selected as the recommendation. **Patrick confirms or swaps.**
**Done when:** the 4 ideas are logged in 9.1; the other 6 go to the backlog (10.4) and the roadmap.

### PHASE C: PLAN DOCS (Planner writes; Patrick reviews; ~25 min)

#### Step 5: PRD + data model + data story
- **`PRD.md`:**
  - problem with baseline numbers
  - 2–3 personas
  - user stories with **Given/When/Then** acceptance criteria and test IDs
  - the 4 ideas, split into Must/Should
  - acceptance checklist, prototype statement, out of scope
- **`DATABASE.md`:**
  - tables and relationships (ER diagram)
  - agent read-only grants
  - vector table (if needed)
- **`DEMO_DATA.md` + generator YAML:**
  - volumes
  - India-realistic values
  - **story beats** for each hero idea (Part 12)

#### Step 6: Architecture + agents + security + tests
- **`ARCHITECTURE.md`:**
  - diagram (Mermaid)
  - services and ports
  - API list
  - SSE events
  - model mapping
  - cost note
- **`AGENTS.md`:** per agent:
  - role, model role, tools, trigger
  - output schema, guardrails, approvals
  - 10–15 eval questions
- **`SECURITY.md`:** roles, consent, agent limits, secrets
- **`TESTING.md`:** test IDs for every acceptance criterion, E2E journeys, evals, attack prompts

#### Step 7: Design applied + tailored build prompts
- **`DESIGN_SYSTEM.md`:** Part 8 applied to this use case:
  - screens
  - Home bento tiles
  - icon rail items
  - name and logo
- **`BUILD_PROMPTS.md`:** BP-04 → BP-12 rewritten with the real entities, screens, ideas and tests.

**Patrick confirms:** the product name, the screen list and any open design choice.

#### Step 8: GATE (Patrick, 5 min)
| Check | ✅ |
|---|---|
| Skeleton running; `make check` green (BP-01 → BP-03) | ☐ |
| Model mapping confirmed and tested | ☐ |
| 4 ideas confirmed; PRD stories with Given/When/Then | ☐ |
| Data model + story beats + generator config ready | ☐ |
| Agents, guardrails, eval questions written | ☐ |
| Design (name, logo, screens) confirmed | ☐ |
| Time on budget, or cuts agreed | ☐ |

**Done when:** every box is ticked and Patrick says **"go"**.

### PHASE D: BUILD (Claude Code runs the tailored prompts; Definition of Done on every prompt)

#### Step 9: Data + API + screens (BP-04 → BP-06, 45 min)
- **BP-04, data:**
  - generator, validation checks, golden answers
  - `make data-reset`
- **BP-05, API:**
  - endpoints, role checks
  - tests for every Must story
- **BP-06, screens:**
  - Home bento, list, record view, copilot drawer
  - all states (empty, error, loading)
  - Playwright journeys + axe

**Done when:** `make check` is green and the screens show the story data.

#### Step 10: AI ideas (BP-07 → BP-10, 55 min)
Build order: **hero 1 → hero 2 → supporting 1 → supporting 2**. Each idea gets:
- its agent graph and tools (read-only first)
- structured output
- its UI surface (streaming, sources, approval card)
- evals and attack prompts
- an audit trail entry

**Checkpoint at T+110:** hero 1 works end to end. If not, the Planner proposes cuts (Rule Zero).
**Done when:** each idea passes its evals (≥ 90% on the hero ideas) and its E2E journey.

### PHASE E: FREEZE AND TEST

#### Step 11: Feature freeze
No new features. New ideas go to the backlog (10.4).

#### Step 12: Full test run + UAT + fixes (BP-11, 25 min)
**Builder:** runs `make check-full` (all tests, all evals, data checks, attack prompts, accessibility) and fixes failures.
**Patrick:** runs the UAT checklist (11.4) as each persona.
**Done when:** everything is green, or known issues are written down with workarounds; reports are saved to `docs/test-reports/`.

### PHASE F: FINAL

#### Step 13: Final docs + investment pack (Planner, in parallel with Step 12)
1. Patrick uploads the current `docs/` folder (zipped) to this chat.
2. The Planner updates the docs to match what was built.
3. The Planner writes the customer pack:
   - overview
   - architecture
   - AI agents
   - API
   - test results
   - user guide
   - run guide (how to start the containers)
   - security
   - roadmap
4. The Planner writes the **investment pack** (13.3).

#### Step 14: Demo readiness (BP-12, 15 min)
**Builder:**
- runs `make data-reset` then `make demo-check`
- tags `v1.0-demo`
- writes the start/stop instructions into `README.md`

**Patrick:**
- runs the demo script once (13.2)
- records a **backup video**
- packs the venue kit: charger, hotspot, adapters, and the laptop with Docker Desktop set to start on boot

**Done when:** the demo runs from a cold start (laptop restart → `make up` → ready) in under 3 minutes.

**Tomorrow morning (no building, only start-up):** start Docker Desktop → `make up` → `make demo-check` → present.

---

## PART 7: AI LIBRARY

### 7.1 General ideas bank (any use case)
| # | Idea | Wow moment | Effort |
|---|---|---|---|
| G1 | **Talk to your data** | Question → agent writes SQL → **right chart drawn live** with sources | M |
| G2 | **Generative tile** | "Show me X by Y" → **a new bento tile appears** | M |
| G3 | **"Why did this change?"** | Click a spike → cause explained with evidence | M |
| G4 | **Anomaly watchdog** | Unusual numbers flagged with an explanation | M |
| G5 | **What-if simulator** | Move a slider → forecast impact with a range | M–L |
| G6 | **Forecast** | 30/90-day forecast; risks narrated | M |
| G7 | **Daily AI brief** | The 3 things that matter today, each with **Do it** | S–M |
| G8 | **Action agent with approval** | Issue spotted → fix drafted → **Approve** → done | M |
| G9 | **Document intelligence** | Drop a PDF/image → data extracted into the app | M |
| G10 | **Knowledge copilot** | Answers from their documents **with citations** | S–M |
| G11 | **Voice / multilingual** | Tamil, Hindi or English, by voice | M |
| G12 | **Self-checking answers** | A second agent re-checks numbers; "verified" badge | M |
| G13 | **Next best action** | Ranked next step per record | M |
| G14 | **Data quality fixer** | Finds duplicates/gaps; fixes after approval | S–M |
| G15 | **One-click report** | Summary report/PDF with charts and narrative | S–M |
| G16 | **AI audit trail + cost** | Every step, tool, data touched, tokens, time | S |
| G17 | **Persona-aware answers** | Same question → manager summary vs operator checklist | S |
| G18 | **Value meter** | Live tile: hours saved / value protected by the AI | S |

### 7.2 CRM-style ideas (if the use case is sales/customer-facing)
| # | Idea | Wow moment | Effort |
|---|---|---|---|
| C1 | **Deal risk radar** | Risk score with reasons + one-click rescue plan | M |
| C2 | **Relationship health** | Health ring per account that explains itself | M |
| C3 | **Lead scoring + routing** | Scored, enriched, assigned in seconds with reasons | S–M |
| C4 | **Meeting prep brief** | One card before a call | S |
| C5 | **Notes → CRM autopilot** | Notes/recording → summary, stage update, tasks (approved) | M |
| C6 | **Context-aware email draft** | Draft that knows the history | S |
| C7 | **Pipeline what-if** | "What if we close 3 of the top 5?" | M |
| C8 | **Churn early warning** | Accounts likely to leave + save action | M |
| C9 | **Next best action per rep** | 5 highest-impact actions per day | M |
| C10 | **Inbox copilot** | Messages classified + suggested replies | M |

### 7.3 Agent building blocks and safety rules
| Agent | Model role | Tools | Approval |
|---|---|---|---|
| Router / orchestrator | Fast (route) / Planner (multi-step) | Other agents | No |
| Data Q&A (text-to-SQL) | Worker | Read-only SQL, schema, chart spec | No |
| Insights / root cause | Worker | SQL, stats, chart spec | No |
| Watchdog / scorer | Fast + Worker | SQL, stats | No |
| Forecast / what-if | Worker + Python | Forecast functions, SQL | No |
| Action agent | Worker | Email (Mailpit), tasks, DB write (separate role) | **Always** |
| Report writer | Worker | SQL, charts, PDF | Before sending |
| Document extraction | Worker (vision, if available) | File reader | Before saving |
| Knowledge (RAG) | Worker + Embeddings | Vector search, citations | No |
| Verifier | Fast | SQL re-check | No |

**Safety rules (into `AGENTS.md` + `SECURITY.md`):**
1. **Read-only DB user** for agents: `SELECT` on an allowlist of tables, 5 s statement timeout, 1,000-row limit.
2. **The user's role** goes with every tool call; data is filtered by role.
3. **Writes only through the Action agent**, only after **human approval**, with an **idempotency key** (single-use approvals).
4. **Every answer cites its data** (rows / query / document).
5. **Structured outputs:** every agent returns a validated schema (answer, sources, numbers, chart spec, proposed action), with one retry on failure.
6. **Chart spec:** agent charts follow one JSON schema, validated before rendering.
7. **Prompt-injection defence:** record text and documents are data, never instructions.
8. **Resilience:** timeouts, retries with backoff, fallback to another configured model, a visible "AI is busy" state.
9. **Audit trail:** every step, tool, data touched, tokens and time logged and visible in the UI.
10. **No PII to models** without consent.

### 7.4 Use-case adapter playbook (the Planner runs it at Step 1)
1. Use case → **personas + jobs to be done**
2. Jobs → **entities and relationships**
3. Entities → **KPIs and the questions people ask** (Home tiles + eval questions)
4. KPIs → **screens** (generic skeleton below)
5. Pains → **10 ideas** → 2 hero + 2 supporting
6. Hero ideas → **story beats** (Part 12)
7. Ideas → **agents and tools**
8. Everything → **Given/When/Then + test IDs**
9. Brand → **name, logo, palette tweaks**

**Generic app skeleton (the same for every use case):** login with personas → icon rail + clean header → **Home bento** (AI brief + KPIs) → **list** → **record view** → **copilot drawer** (chat, explain, approvals, audit trail) → settings. Only the domain content changes.

**Domain starter hints:**
| Domain | Core entities | Hero idea candidates |
|---|---|---|
| CRM / sales | Company, contact, deal, activity | Deal risk radar, notes → CRM autopilot |
| Support / helpdesk | Customer, ticket, message, SLA | Triage + suggested reply, SLA breach predictor |
| Inventory | Product, warehouse, movement, supplier, PO | Stock-out warning + drafted PO |
| HR / recruitment | Candidate, job, application, interview | Screening with reasons, interview brief |
| Finance AR/AP | Customer, invoice, payment | Collections prioritiser + drafted reminders |
| Field service | Site, asset, work order, technician | Smart dispatch, failure prediction |
| Clinic operations (synthetic) | Patient, appointment, doctor | No-show predictor + reminders |

---

## PART 8: DESIGN SYSTEM ("Mineral Glass"), copied into `DESIGN_SYSTEM.md`

> A calm, light, professional workspace: frosted glass over a soft mineral mist, bento tiles sized by importance, aubergine ink instead of black, jade for action, apricot for "look here". **No dark blue or navy anywhere.** If the customer has brand colours, they replace Jade and Apricot; the structure stays.

### 8.1 Inspiration and what we avoid
**What we take:**
- Refined glass (Apple Liquid Glass, visionOS): glass on the chrome only
- Bento grids: tile size = importance, with one hero tile
- Modern CRMs (Attio, folk): calm density
- Command-first apps (Linear, Raycast): ⌘K keeps the header empty
- Soft mesh "digital lavender" behind the glass, never on data
- Variable type with tabular numbers

**Avoid:**
- Navy or midnight backgrounds with cyan accents
- Inter + default blue + identical cards
- The ✨ sparkle for AI, and letter-in-a-square logos
- Crowded headers and ALL-CAPS labels
- Fade-up on every card, and gradients on data

### 8.2 Colour (contrast checked)
| Token | Hex | Use |
|---|---|---|
| `--canvas` | `#F3F4F0` | Background under the mist |
| `--ink` | `#2A1B33` | Main text (14.6 : 1) |
| `--ink-muted` | `#5E5468` | Secondary text (6.5 : 1) |
| `--jade` | `#0F7A60` | Primary buttons, links, positive, active (5.3 : 1) |
| `--apricot` | `#F2A65A` | Highlight, AI glow, attention (never text) |
| mist | `#E4DDF4` / `#D3EBE1` / `#FCE6D0` | Background mesh |

- **Semantic:** success `#0F7A60` · warning `#A16207` · danger `#BE2F55` · info `#5B4BC4`
- **Chart series:** `#0F7A60`, `#5B4BC4`, `#C9752A`, `#BE2F55`, `#7C9A84`, `#8A5A8F`
- **Dark mode ("Aubergine Night"):** canvas `#1C1322` · ink `#F1EDF5` · muted `#B3A9BD` · jade `#4FD1A5` · apricot `#F5B57A`

### 8.3 Typography
- **Hanken Grotesk** (variable) for all UI text, with tabular numbers
- **Unbounded 600** for the product name only
- **Noto Sans Tamil / Devanagari** as fallbacks
- **Scale:** 12 · 14 (body) · 16 · 20 · 25 · 31 (page heading) · 39 (hero number)
- Sentence case everywhere

### 8.4 Product name and logo
**Name (chosen at Step 7):**
- **Kinlo** (*kin* + *flow*; for relationship-style use cases)
- **Tessel** (tiles that fit together)
- **Orvia** (*orbit* + *via*)
- or a name derived from the use case

The Planner checks the chosen name isn't taken by a well-known product.

**Wordmark:** lowercase Unbounded 600; the "i" dot is the apricot seed from the logo.
**Logomark ("Leaf and seed"):** a jade leaf curving towards an apricot seed. It doubles as the AI copilot button, and the seed pulses while an agent works.
```svg
<svg viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg" aria-label="Kinlo">
  <path d="M5 27C5 14.85 14.85 5 27 5C27 17.15 17.15 27 5 27Z" fill="#0F7A60"/>
  <circle cx="24" cy="24" r="4" fill="#F2A65A"/>
</svg>
```

### 8.5 App shell
```
┌────┬──────────────────────────────────────────────────────────┐
│    │  ◢● kinlo     Pipeline                                   │ ← logo + name + page heading only
│ ⌂  │               Q4 2026, all regions                       │   + one small detail line
│ ▽  ├──────────────────────────────────────────────────────────┤
│ ☏  │            page content (bento / list / record)          │
│ ▦  │                                                          │
│ ☑  │                                                    ◢●    │ ← copilot (logomark), ⌘J
│ ⌕  │                                                          │
│ ⚙  │                                                          │
│ (P)│                                                          │
└────┴──────────────────────────────────────────────────────────┘
 72 px glass rail, icons only
```
- **Icon rail:** always icons (Phosphor duotone, 24 px), each with a tooltip and `aria-label`. The active item gets a jade-tinted glass square and an apricot seed on the rail edge.
- **Header:** always clean: logomark, wordmark, page heading and one detail line. Nothing else.
- **Login:** a single glass card, plus a persona picker for the demo.

### 8.6 Home bento (adapted per use case)
```
 cols →  1   2   3   4   5 │ 6   7   8   9 │10  11  12
row 1  ┌───────────────────┬───────────────┬───────────┐
       │  AI brief (HERO)  │ Main KPI      │ KPI 2     │
row 2  │  today's 3 moves  │ + trend       ├───────────┤
       │  each with Do it  │               │ Value     │
row 3  ├───────────────────┴───────┬───────┴ meter ────┤
       │ Hero idea 1 tile          │ Hero idea 2 tile   │
row 4  │                           │                    │
       └───────────────────────────┴────────────────────┘
```

### 8.7 Glass and bento rules
```css
.glass { background: rgb(255 255 255 / 0.55); backdrop-filter: blur(20px) saturate(140%);
  border: 1px solid rgb(255 255 255 / 0.7);
  box-shadow: inset 0 1px 0 rgb(255 255 255 / 0.8), 0 1px 2px rgb(42 27 51 / 0.06), 0 12px 32px rgb(42 27 51 / 0.08); }
.surface { background: rgb(255 255 255 / 0.82); }
@supports not (backdrop-filter: blur(1px)) { .glass { background: rgb(255 255 255 / 0.92); } }
@media (prefers-reduced-transparency: reduce) { .glass, .surface { background: #FFFFFF; backdrop-filter: none; } }
```
- **Glass:** only on the rail, header, tile frames, drawer and modals. Tables, forms and long text sit on `.surface`.
- **Bento:** 12 columns, 16 px gap.
- **Radius by size:** 28 / 22 / 16 / 10 / 12.
- **One hero tile** per screen.
- **DOM order** = reading order.

### 8.8 Components, motion and quality floor
**Components**
- Buttons: primary jade, secondary glass, ghost. Labels name the action, and the toast repeats it.
- Chips carry text plus an icon.
- Empty states: one line plus one button.

**Motion**
- One page-load sequence, plus the copilot seed pulse.
- `prefers-reduced-motion` is respected.

**Quality floor**
- Contrast ≥ 4.5:1.
- Visible focus ring.
- Glass fallback.
- Works from 360 px phone width to desktop.

---

## PART 9: LOGS AND RISKS

### 9.1 Decisions log
| # | Date | Decision | Made by |
|---|---|---|---|
| D1 | 14 Oct | Docs-first: working docs before code | Patrick |
| D2 | 14 Oct | Plan up to architecture + agents first; final docs last | Patrick |
| D3 | 14 Oct | Design: glassmorphism + bento, no dark blue, icon-only rail, clean header, unique name and logo | Patrick |
| D4 | 14 Oct | This file is the master plan; every prompt follows Part 1 | Patrick |
| D5 | 14 Oct | Progressive project: every change through Part 10 with docs updated without fail | Patrick |
| D6 | 14 Oct | Review gaps fixed; investment-confidence plan | Patrick |
| D7 | 14 Oct | Tests from day zero; managed, story-driven test data | Patrick |
| D8 | 14 Oct | Enterprise technical review applied | Patrick |
| D9 | 14 Oct | **Rule Zero: always interactive** | Patrick |
| D10 | 14 Oct | Default stack confirmed (FastAPI + Next.js + PostgreSQL/pgvector + LangGraph) | Patrick |
| D11 | 14 Oct | **Local only**; no GitHub, no cloud deploy | Patrick |
| D12 | 14 Oct | Builder = **Claude Code in VS Code** (Pro); this chat = Planner | Patrick |
| D13 | 14 Oct | **Everything today in ~3.5 h** after the use case arrives; demo tomorrow; no work tomorrow | Patrick |
| D14 | 14 Oct | Pro plan; the planning workspace can't install packages, so all code runs on the laptop | Patrick |
| D15 | 14 Oct | **Models provided at the lab**; app is model-agnostic; roles mapped at Step 2 | Patrick |
| D16 | 14 Oct | **Run as Docker containers locally on ports** | Patrick |
| D17 | 14 Oct | Before the use case: **docs and prompts only** | Patrick |
| D18 | 14 Oct | **Solo: Patrick + Claude Code** | Patrick |
| D19 | 14 Oct | **Windows** laptop (WSL2) | Patrick |
| D20 | 14 Oct | **Small single use case**: right-size, not a full enterprise build (Part 14) | Patrick |
| D21 | 14 Oct | **5 hero + 5 supporting candidates → pick 2 hero + 2 supporting** | Patrick |
| D22 | 14 Oct | **Build the kit at the lab** once VS Code + Claude Code are logged in (not before) | Patrick |
| D23 | 14 Oct | **Claude Code in VS Code builds the kit itself**; the Planner only hands over the plan + `VSCODE_HANDOFF.md` | Patrick |

### 9.2 Change log
| # | Change | Version |
|---|---|---|
| 1–7 | v1 → v7: plan, design, master plan, progressive delivery, gap fixes, investment plan, testing, data, enterprise review | v1–v7 |
| 8 | Rule Zero at the top | v7.1 |
| 9 | Environment decisions D10–D14 logged | v7.2 |
| 10 | **Re-planned for today:** solo + Claude Code, Windows/WSL2, local containers, model-agnostic, ~3.5 h timeline, 2+2 ideas, right-sized scope, build kit | **v8** |
| 11 | Kit build moved to the lab (D22) | v8.1 |
| 12 | Kit built by Claude Code from the handoff (D23) | v8.2 |

### 9.3 Open questions
| # | Question | Needed by |
|---|---|---|
| Q1 | The use case | Step 1 (this afternoon) |
| Q2 | Available models and keys (at the lab) | Step 2 |
| Q3 | Is the laptop available before the use case, to install the tools (A1)? | A1 |
| Q4 | Will the customer join tomorrow's demo in person, or on a screen share? | Step 14 |

### 9.4 Risks
| # | Risk | L | I | Response |
|---|---|---|---|---|
| R1 | Use case vague or bigger than 3.5 h | M | H | Adapter playbook; assumptions confirmed; cut order (5.1) |
| R2 | Available models are weak at tool calling | M | H | `make models-check`; best model as Worker; simpler single-agent flows |
| R3 | Docker/WSL issues on Windows | M | H | Install early (A1); `docker run hello-world`; fallback: API/web natively in WSL with Postgres in Docker |
| R4 | Pro usage limits hit mid-build (shared by this chat and Claude Code) | M | H | Keep the planning chat short during the build; build prompts are self-contained so they can be pasted into another tool if needed |
| R5 | Agent gives a wrong number in the demo | M | H | Verifier; sources shown; evals ≥ 90%; rehearsed questions |
| R6 | Demo laptop fails tomorrow | L | H | Backup video; cold-start test; charger; repo copied to a second laptop |
| R7 | No internet at the venue (models are cloud APIs) | M | H | Mobile hotspot; cached responses for the rehearsed questions (`DEMO_CACHE=on`, clearly labelled) + backup video |
| R8 | Demo data looks fake | M | H | Part 12 generator + story beats + checks |
| R9 | Docs drift from code | M | M | Definition of Done + docs guard in `make check` |
| R10 | Keys leak | L | H | `.env` only; gitleaks in `make check` |

---

## PART 10: CHANGES AND NEW IDEAS (progressive project)

### 10.1 Change pipeline (every change, even small ones)
1. **Capture** the change in the backlog (10.4) or the change log (9.2).
2. **Assess impact** (10.2), then **ask Patrick** (Rule Zero).
3. **Update the docs first.**
4. **Build** it with Claude Code.
5. **Run `make check`.**
6. **Record** it in the logs, the snapshot and the version.

During the freeze, only fixes go in; new ideas go to the backlog.

### 10.2 Impact → docs to update
| Change touches | Update |
|---|---|
| Scope, stories, KPIs | `PRD.md` |
| Screens, components, tokens, name/logo | `DESIGN_SYSTEM.md` |
| Services, APIs, ports, models, versions | `ARCHITECTURE.md` |
| Tables, fields, data, story beats | `DATABASE.md` + `DEMO_DATA.md` + generator config |
| Agents, prompts, tools, guardrails | `AGENTS.md` (+ evals) |
| Roles, data handling, consent | `SECURITY.md` |
| Tests | `TESTING.md` |
| **Anything** | **This file** (snapshot, tracker, logs) |

### 10.3 Definition of Done (every build prompt and every change)
- [ ] Docs in 10.2 updated (version + date in their header)
- [ ] Tests added or updated; `make check` green
- [ ] Architecture diagram and API list still match the code
- [ ] Local git commit with a clear message (tag at milestones)
- [ ] This file's snapshot, tracker and logs updated
- [ ] Any open question was asked and answered (Rule Zero)

`make check` includes a **docs guard**: it fails if any of these changed since the last commit without their doc:
- `api/agents/**` without `docs/AGENTS.md`
- API routes without `ARCHITECTURE.md`
- models or migrations without `DATABASE.md`
- `web/` components or styles without `DESIGN_SYSTEM.md`

### 10.4 Idea backlog
| ID | Idea | Source | Value | Effort | Status |
|---|---|---|---|---|---|
| I-001 | | | | | New |

### 10.5 After the demo
Unchosen ideas, customer feedback and the deferred items (Part 14) become the **roadmap**. Each later phase repeats Steps 5–14 through this pipeline.

---

## PART 11: TESTING (from the first prompt)

### 11.1 Test layers (right-sized)
| Layer | Tool | Covers |
|---|---|---|
| Unit | pytest, vitest | KPI logic, tool functions, components |
| API | pytest + httpx | Every Must story's Given/When/Then; role checks; bad input |
| E2E | Playwright (+ axe) | 2–3 persona journeys incl. an approved action; accessibility |
| AI evals | pytest eval harness | 10–15 questions per hero idea, 5 per supporting idea; numbers match golden answers; correct tools; approvals respected |
| AI security | Attack-prompt suite (~10) | Prompt injection, role leakage, forbidden SQL |
| Data | Validation checks | Integrity, ranges, story beats present (Part 12) |
| Hygiene | ruff, eslint, typecheck, gitleaks, docs guard | Code quality, secrets, docs in sync |

### 11.2 Commands
| Command | Runs | When |
|---|---|---|
| `make check` | Hygiene + unit + API + data + eval smoke (hero questions) + Playwright smoke + docs guard | **End of every build prompt** |
| `make check-full` | Everything incl. all evals, all E2E, attack prompts, axe | Step 12 and before the demo |
| `make models-check` | Tool calling, JSON, latency per configured model | Step 2 |
| `make demo-check` | Data reset + smoke + hero evals + hero E2E journeys | Tomorrow before presenting |

### 11.3 Gates (a step isn't done unless all pass)
- All tests pass.
- Hero evals ≥ 90%, with 0 invented numbers and 0 unapproved actions.
- 0 secrets found.
- 0 critical accessibility issues.
- Data checks green.
- Docs guard green.

### 11.4 UAT checklist (Patrick, Step 12)
- [ ] A first-time user finds the main insight in under 1 minute
- [ ] Each persona completes their top task unaided
- [ ] Natural questions work (typos, follow-ups, vague questions)
- [ ] Every AI answer shows its sources; it's clear *why*
- [ ] Approve / reject works, and it's clear what the AI did
- [ ] A user can't see another role's data, even by asking the agent
- [ ] Empty, error and slow states are friendly
- [ ] Text on glass is readable; the icons have tooltips
- [ ] Mocked integrations are labelled
- [ ] The demo cold start takes under 3 minutes

### 11.5 Test management
- Every test ID links to a story or risk (`TESTING.md`).
- Evals use fixed settings (temperature 0) on the frozen demo dataset.
- Golden answers are computed from the data (12.5).
- Reports go to `docs/test-reports/` for the customer pack.

---

## PART 12: TEST AND DEMO DATA (managed, enterprise-quality)

### 12.1 Principles
- **Synthetic by default.** Fake identifiers are obviously fake (e.g. `example.com`).
- **Deterministic.** A fixed seed gives the same data every time.
- **India-realistic:**
  - Cities: Chennai, Bengaluru, Mumbai, Delhi NCR, Hyderabad, Pune.
  - Indian names and company styles.
  - INR in lakh/crore.
  - +91 phone format.
  - IST hours and seasonality.
- **Consistent.** Every reference resolves, totals reconcile, and the dates make sense.
- **Alive.** Dates are relative to *today*, so recent periods always have activity.
- **Story-driven.** Named **story beats** give the hero ideas something real to find.
- **Validated.** Checks run after every load and in `make check`.
- **Managed.** Versioned YAML config + manifest (seed, counts, version); changes go through Part 10.

### 12.2 Datasets
| Set | Purpose | Size |
|---|---|---|
| **Fixtures** | Unit tests | Tens of rows, hand-written in `tests/fixtures/` |
| **Demo** | The demo, and the API/E2E tests | Mid-size business scale (e.g. thousands of main records, 12–18 months of history), set per use case |
| **Eval golden** | Frozen copy of Demo + computed golden answers | = Demo |
| **Edge** | Nulls, duplicates, Tamil/Hindi Unicode, long text, injection text inside records, zero/negative values, month-end dates | Hundreds of rows; used by tests and attack prompts |

### 12.3 Generator (`scripts/datagen/`)
**YAML config per use case:**
- Entities, volumes and relationships.
- Realistic distributions and seasonality.
- Personas and roles.
- **Story beats.**

**Outputs:** the database load, plus `manifest.json` (dataset version, seed, row counts, hash).

**Commands:**
- `make data-gen`
- `make data-reset` (under 1 minute)
- `make data-check`

### 12.4 Story bible (`docs/DEMO_DATA.md`)
Each story beat has:
- an ID
- the persona and narrative
- the records involved
- what the AI should find and recommend
- the demo step it supports
- the tests that check it

The demo script is written from this file, so the demo, the data and the tests tell the same story.

### 12.5 Golden answers are computed
When the data is generated, the SQL behind each eval question is run and the expected answer is stored, so evals never go stale.

### 12.6 Real customer data
- Used only with consent, through an import step with anonymisation.
- Kept separate from the synthetic data.
- Deleted after the demo unless agreed.

---

## PART 13: WINNING THE CUSTOMER'S CONFIDENCE

### 13.1 Three things to prove
1. **"They understood us":**
   - their words and KPIs
   - their pain in their own numbers
   - their branding
2. **"It actually works":**
   - live hero flows on realistic data
   - approvals, sources and passing tests shown live
3. **"They can take it further":**
   - clean architecture and a security model
   - tests and an audit trail
   - honest labels and a roadmap

### 13.2 Demo script (~12 min, written at Step 13 from `DEMO_DATA.md`)
1. **Their pain today**, in their numbers (1 min).
2. **Log in as their persona.** The Home bento shows the AI brief with its 3 moves (2 min).
3. **Hero 1, end to end:** why → sources → drafted action → approve → the value meter moves (3 min).
4. **Hero 2, end to end** (3 min).
5. **Supporting ideas**, quickly; then a free question, and a role switch to show permissions (2 min).
6. **Under the hood:** audit trail with tokens/time, the `make check-full` results, and the architecture on one slide (1 min).
7. **Roadmap and next step:** a pilot (30 s).

### 13.3 Investment pack (Step 13)
- **One-page summary:** the problem, what we built, the results.
- **ROI estimate** in their numbers, with the assumptions stated.
- **Proof of quality:** test results and eval scores.
- **Security and privacy approach.**
- **Architecture** and how it scales.
- **Roadmap:** the unchosen ideas plus Part 14's deferred items.
- **Proposed pilot:** scope, success measure (their KPI) and timeline.

### 13.4 Tough questions
| They ask | We show |
|---|---|
| "Will the AI make things up?" | Sources on every answer, the verifier, eval scores |
| "Is our data safe?" | Read-only agent access, role filtering, approvals, audit trail, consent |
| "What if it does something wrong?" | Every action needs approval; audit trail |
| "Which AI does it use? Are we locked in?" | Models are configuration; works with Azure, AWS, Google, OpenAI or Anthropic |
| "What does it cost to run?" | Tokens per query from the audit trail → cost estimate |
| "Can it connect to our systems?" | Integration labels + roadmap |

---

## PART 14: SCOPE: KEPT, RIGHT-SIZED, DEFERRED (single use case, solo, local)

| Kept fully | Right-sized for today | Deferred to the roadmap (shown in the investment pack) |
|---|---|---|
| Master plan + Rule Zero + change pipeline | 8 working docs at 1 page each | Cloud deploy, separate environments, preview builds |
| Design system (glass + bento, name, logo) | Auth: 2–3 demo personas with JWT | SSO, multi-tenancy, full row-level security policies |
| Agent guardrails: read-only DB user, limits, approvals, idempotency, structured outputs, sources, injection defence | Tests: unit + API + 2–3 E2E journeys + evals + ~10 attack prompts | Load testing, ZAP/Trivy/Semgrep scans, SBOM, pen test |
| Managed, story-driven synthetic data + checks | `make check` instead of cloud CI | GitHub Actions CI, branch protection |
| Model-agnostic AI layer + model check | Built-in AI audit trail | Langfuse, Sentry, uptime monitoring, alerting |
| Docker Compose with health checks | Local git tags for releases/rollback | Terraform/IaC, backups/DR, India-region hosting |
| Investment pack + demo script | i18n/voice only if an idea needs it | Full multilingual UI, voice |

---

## PART 15: READINESS CONFIRMATION (v8)

| Area | Ready? | How |
|---|---|---|
| Building from a short use case alone | ✅ | Adapter playbook (7.4), generic skeleton, domain hints, Rule Zero questions |
| Any AI provider | ✅ | Model-agnostic layer + `make models-check` + role mapping at Step 2 |
| Windows, local containers | ✅ | A1 install guide, WSL hygiene, Docker Compose with health checks |
| One person in ~3.5 h | ✅ | Skeleton built in parallel with planning; tailored, self-contained build prompts; cut order |
| Quality | ✅ | Tests from the first prompt, `make check` gates, evals, UAT |
| Demo data | ✅ | Generator, story beats, checks, computed golden answers |
| Docs always in sync | ✅ | Definition of Done + docs guard |
| Demo tomorrow with no work possible | ✅ | Cold-start test, `make demo-check`, backup video, offline cache, venue kit |
| Winning confidence | ✅ | Demo script, investment pack, tough-question answers |

**Dependencies still open:** the use case (this afternoon), the available models and keys (at the lab), and the laptop for the A1 installs (Q3).
