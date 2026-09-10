# ❓ Open Questions

> **Stage 1: Real Unknown** — Document the specific questions and unknowns that this project must answer.

---

## 📋 Active Unknowns
*List the questions that need answers before or during the development process. As they are resolved, link to the formula, design, or code that answers them.*

| Question | Owner / Agent | Target Stage for Resolution | Resolution Notes / Link |
| :--- | :--- | :--- | :--- |
| **Q1:** Does the Codespaces default machine size (2-core) run minikube + Zarf init acceptably, or is a bigger machine type required? | Environment Agent | `2_Environment` | Not yet tested in an actual Codespace — this PoC ran on a local macOS machine. See R-001 in `risks.md`. |
| **Q2:** Should the package eventually be published to an OCI registry (`zarf package publish`) instead of only built/deployed locally? | Human | `4_Formula` | Open — tracked as TSK-018 in `kanban.md`. |
| **Q3:** Do we need to demonstrate an actual air-gapped transfer (moving the `.tar.zst` to a disconnected environment), or is connected build+deploy sufficient to satisfy the OKRs? | Human | `1_Real_Unknown` | Explicitly out of scope per `problem_statement.md`; tracked as TSK-017 if the scope expands. |

---

## ✅ Resolved

| Question | Resolution |
| :--- | :--- |
| What Kubernetes distro should back the cluster? | minikube with the Docker driver — matches the objective ("environment is codespaces... minikube") and is what was actually verified working. |
| Where does the private package source live? | `5_Symbols/zarf-hello-world/` (RULE-005 — source code lives in `5_Symbols`). |

---

## 📌 Instructions
1. Document questions **before** writing code.
2. Update the "Resolution Notes" column as soon as a decision is made or implemented.
3. Move fully resolved questions to the ✅ Resolved table above once answered.
