# 🗂 Project Risks

> **Stage 1: Real Unknown** — Track active risks, solved risks, and the risk update log. Add new risks with every project update and mention those that are solved.

## Risk Matrix

| Severity | Symbol | Meaning |
|----------|--------|---------|
| Critical | 🔴 | Blocks delivery — must resolve immediately |
| High | 🟠 | Significantly impacts quality or timeline |
| Medium | 🟡 | Should be addressed in current milestone |
| Low | 🟢 | Monitor — address when convenient |

---

## ⚠️ Active Risks

### R-001: Codespaces Resource Limits for minikube
- **Status:** 🟡 Active
- **Severity:** Medium
- **Likelihood:** Medium (default Codespaces machine types can be CPU/RAM constrained for a nested Kubernetes cluster)
- **Impact:** minikube may fail to start or run slowly inside a small Codespace, blocking `zarf init` and package deploys.
- **Trigger:** Codespace machine type too small (e.g., 2-core) for `minikube start` + Zarf's init package workloads (registry, agent).
- **Mitigation:** Use a Codespaces machine type with at least 4 cores/8GB RAM; use the Docker driver for minikube; document the required devcontainer resources in `2_Environment/architecture.md`.
- **Last Updated:** 2026-09-10

### R-002: Zarf Init Package Version Drift
- **Status:** 🟢 Active
- **Severity:** Low
- **Likelihood:** Low
- **Impact:** A newer/older public Zarf init package version may behave differently than documented, breaking `zarf init` steps.
- **Trigger:** `zarf init` pulling a different init-package version than the Zarf CLI version installed.
- **Mitigation:** Pin the Zarf CLI version in the devcontainer/setup docs; record the exact version used in `2_Environment/dependencies.md`.
- **Last Updated:** 2026-09-10

### R-003: Secrets/Registry Credentials Handling
- **Status:** 🟢 Active
- **Severity:** Low
- **Likelihood:** Low (PoC has no real secrets yet)
- **Impact:** If registry credentials are later needed for a private package registry, hardcoding them would violate RULE-003/004.
- **Trigger:** Adding a private container registry or external image source to the package.
- **Mitigation:** Any credential needed goes into Azure Key Vault (`/vaults/dp-kv-deliverypilot/secrets`), never into `zarf.yaml` or git.
- **Last Updated:** 2026-09-10

---

## ✅ Solved Risks

*(none yet — this is a fresh project bootstrapped from delivery-pilot-template on 2026-09-10)*

---

## 📋 Risk Update Log

| Date | Update | Risk ID | Change |
|------|--------|---------|--------|
| 2026-09-10 | Project bootstrapped from delivery-pilot-template | R-001 → R-003 | Initial risk assessment for Zarf-in-Codespaces PoC |

---

## Risk Review Cadence

- **Every project update** — Add new risks, update existing ones, move solved risks to the Solved section
- **Every milestone completion** — Review all active risks, re-evaluate severity/likelihood
- **Smoke test failures** — If a smoke test catches a new class of error, create a risk entry
- **Tool changes** — When adding or removing a tool, evaluate and log new risks
