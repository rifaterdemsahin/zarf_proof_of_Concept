# 🗂 Tasks & Phases

> **Stage 1: Real Unknown** — Project phases and task breakdown managed by the **Real Agent**. Each task is assigned to a specific agent. Complex tasks are coordinated by the Real Agent across multiple agents.

## Phase 1: Bootstrap (Completed)

| ID | Task | Agent | Done |
|----|------|-------|------|
| TSK-001 | Bootstrap repo from delivery-pilot-template (7-stage folders, root files, skills) | Real Agent | [x] |
| TSK-002 | Replace template placeholders (PROJECT_NAME, REPO_NAME, PAGES_URL) | Symbols Agent | [x] |
| TSK-003 | Define project goal in problem_statement.md and okrs.md | Real Agent | [x] |

## Phase 2: Environment Setup — Codespaces + minikube + Zarf (In Progress)

| ID | Task | Agent | Coordination | Done |
|----|------|-------|-------------|------|
| TSK-004 | Document Codespaces setup requirements (minikube, Zarf CLI, kubectl) — no root `.devcontainer/` per RULE-005 (ADR-002) | Environment Agent | Real Agent coordinates: Environment documents setup → Formula specs the environment | [x] |
| TSK-005 | Install/verify Zarf CLI and minikube (verified on macOS w/ Docker driver; same steps apply in Codespaces) | Environment Agent | [x] |
| TSK-006 | Start minikube cluster | Environment Agent | [x] |
| TSK-007 | Run `zarf init` against the public Zarf init package | Environment Agent | Real Agent coordinates: Environment runs init → Test Agent smoke-tests cluster state | [x] |

## Phase 3: Private Package — Hello World Website (Completed)

| ID | Task | Agent | Coordination | Done |
|----|------|-------|-------------|------|
| TSK-008 | Design the hello-world website + package layout | Simulation Agent | Real Agent coordinates: Simulation sketches the package structure → Formula specs it | [x] |
| TSK-009 | Write spec for the private Zarf package (SPEC-014 in 4_Formula/specs.md) | Formula Agent | [x] |
| TSK-010 | Author `zarf.yaml` + hello-world manifests in 5_Symbols | Symbols Agent | Real Agent coordinates: Formula spec → Symbols implements zarf.yaml + k8s manifests | [x] |
| TSK-011 | Build the private package with `zarf package create` | Symbols Agent | [x] |
| TSK-012 | Deploy the private package with `zarf package deploy` | Symbols Agent | [x] |

## Phase 4: Testing & Showcase (Completed)

| ID | Task | Agent | Coordination | Done |
|----|------|-------|-------------|------|
| TSK-013 | Verify hello-world site is reachable (port-forward / minikube service) | Test Agent | Real Agent coordinates: Test Agent verifies → Semblance logs any errors | [x] |
| TSK-014 | Run smoke tests / nav-sync / structural validation | Test Agent | [x] |
| TSK-015 | Publish retrospective in 6_Semblance/lessons_learned.md | Semblance Agent | Real Agent coordinates: gathers lessons from all agents → Semblance compiles → feeds back to Real Agent | [x] |
| TSK-016 | Draw the Zarf-on-minikube architecture as a versioned SVG in 3_Simulation | Simulation Agent | [x] |

## Task Management Rules

1. **Real Agent owns this file** — breaks the project into phases and tasks, assigns agents, coordinates complex tasks
2. **Every task names its agent** — the Agent column identifies which stage agent is responsible for execution
3. **Complex tasks describe coordination** — tasks involving 2+ agents include a Coordination column explaining how the Real Agent orchestrates the workflow
4. **Status tracking**: `[ ]` Pending, `[x]` Completed, `[~]` In Progress, `[!]` Blocked
5. **Link to specs** — tasks that implement a spec should reference the SPEC-XXX number
6. **Task granularity** — a task should be completable in a single coding session
7. **Real Agent as coordinator** — for complex tasks, the Real Agent defines the scope, dispatches to agents, and validates the result against OKRs
