# 📋 Project Kanban Board

> **Stage 1 of 7 (Real Unknown):** Track setup tasks, ongoing development, and pilot status.
> This file is a live Kanban board. AI agents and human developers must keep this updated as they do their work.

---

## 📖 How to Use This Kanban

1. **Move Tasks**: Move task items between sections (`Backlog 📥`, `Planned 📋`, `In Progress 🔄`, `In Review 👀`, `Done ✅`) as work progresses.
2. **Assignee**: Designate who is working on the task (e.g., `Gemini`, `Claude`, `Copilot`, `Kilo Code`, or `Human`).
3. **Traceability**: Link each task to its relevant stage documentation or source code (e.g., referencing a setup guide in `2_Environment` or a validation check in `7_Testing_Known`).
4. **Update Logs**: When an AI agent performs a task, they must update this kanban board in the same commit to ensure real-time status accuracy.

---

## 📥 Backlog
*Tasks that are defined but not yet scheduled.*

- [ ] **TSK-017: Air-gapped transfer demo**
  - **Assignee:** Human / Environment Agent
  - **Details:** Demonstrate moving the built `.tar.zst` package to a disconnected environment and deploying it there, to actually exercise Zarf's air-gap story (this PoC only proved connected build/deploy).
  - **Stage Reference:** [1_Real_Unknown/problem_statement.md](problem_statement.md) (explicitly out of scope for the first pass)

- [ ] **TSK-018: Publish the package to a registry**
  - **Assignee:** Human
  - **Details:** Push `zarf-package-hello-world-*.tar.zst` to an OCI registry (e.g. `zarf package publish`) instead of only building locally.
  - **Stage Reference:** [5_Symbols/zarf-hello-world/README.md](../5_Symbols/zarf-hello-world/README.md)

---

## 📋 Planned / To Do
*Tasks scheduled for implementation.*

*Nothing currently planned beyond the backlog above — Objectives 1 & 2 are both achieved (see `okrs.md`).*

---

## 🔄 In Progress
*Active tasks currently being worked on.*

*No active tasks in progress.*

---

## 👀 In Review
*Tasks completed and awaiting validation/review.*

*Nothing pending review.*

---

## ✅ Done
*Verified and completed tasks.*

- [x] **TSK-001: Bootstrap from delivery-pilot-template**
  - **Assignee:** Claude
  - **Details:** Copied the 7-stage scaffold, replaced placeholders, defined project-specific problem statement/OKRs/tasks/risks.
  - **Stage Reference:** [1_Real_Unknown/problem_statement.md](problem_statement.md)

- [x] **TSK-004–007: Zarf CLI + minikube + zarf init**
  - **Assignee:** Environment Agent (Claude)
  - **Details:** Installed Zarf CLI (`defenseunicorns/tap/zarf`), verified minikube cluster Ready, ran `zarf init` against the public init package. `zarf` namespace pods (`zarf-injector`, `zarf-docker-registry`, `agent-hook` x2) all Running.
  - **Stage Reference:** [2_Environment/codespaces_zarf_setup.md](../2_Environment/codespaces_zarf_setup.md)

- [x] **TSK-008–012: Private hello-world Zarf package**
  - **Assignee:** Symbols Agent (Claude)
  - **Details:** Authored `zarf.yaml` + K8s manifests, built with `zarf package create`, deployed with `zarf package deploy`. Found and fixed a missing `<meta charset="utf-8">` bug during visual verification, redeployed.
  - **Stage Reference:** [5_Symbols/zarf-hello-world/](../5_Symbols/zarf-hello-world/), [4_Formula/specs.md](../4_Formula/specs.md) SPEC-014

- [x] **TSK-013–016: Verify & diagram**
  - **Assignee:** Test Agent / Simulation Agent (Claude)
  - **Details:** Verified the hello-world site reachable via `kubectl port-forward` + browser screenshot; ran `nav_sync.py` + `smoke_test.py` (11/11 pass); drew `3_Simulation/zarf_architecture.svg`.
  - **Stage Reference:** [3_Simulation/zarf_architecture.svg](../3_Simulation/zarf_architecture.svg), [6_Semblance/smoke_test_report.md](../6_Semblance/smoke_test_report.md)

---

## ⚙️ Maintenance

- [ ] Go over git commits periodically, reread changed files, and create/update Kanban tasks to stay on track
- [ ] Re-verify the environment steps (`2_Environment/codespaces_zarf_setup.md`) actually inside a fresh GitHub Codespace, not just locally on macOS
- [ ] Keep `3_Simulation/zarf_architecture.svg` in sync if the package's namespaces/components change
- [ ] Update `4_Formula/specs.md` SPEC-014 if `zarf.yaml` changes
- [ ] Pay down technical debt noted in the Backlog (air-gapped demo, registry publish) as time allows
