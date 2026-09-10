# 🧪 Validation Report

> **Stage 7: Testing Known** — The final validation layer. Maps every objective, hypothesis, and question from Stage 1 to its outcome and proof of working.

---

## 🗺️ Objective & Hypothesis Mapping

### Objective 1: Run Zarf in GitHub Codespaces on minikube
- **Original Unknown/Question:** Can we stand up a working Zarf + minikube environment so the packaging system can be exercised end-to-end?
- **Test Method:** Installed Zarf CLI, confirmed minikube node Ready, ran `zarf init` against the public init package, checked pod status in the `zarf` namespace.
- **Evidence:** `kubectl get nodes` → `minikube Ready`; `kubectl get pods -n zarf` → `zarf-injector`, `zarf-docker-registry`, `agent-hook` (x2) all `Running`. See `1_Real_Unknown/okrs.md` KR 1.1–1.3.
- **Result:** ✅ Passed (run locally on macOS with the Docker driver — the identical documented steps in `2_Environment/codespaces_zarf_setup.md` have not yet been re-run inside an actual Codespace; see Q1 in `questions.md`)
- **Date Validated:** 2026-09-10

---

### Objective 2: Showcase Zarf's packaging system with a private package
- **Original Unknown/Question:** Can we build and deploy a private Zarf package that proves the packaging workflow works end-to-end?
- **Test Method:** `zarf package create` on `5_Symbols/zarf-hello-world/`, `zarf package deploy` against the initialized cluster, `kubectl get pods/svc -n hello-world`, `kubectl port-forward` + browser screenshot.
- **Evidence:** Deployment `hello-world` `Running`, Service `hello-world` ClusterIP `:80`; `curl http://127.0.0.1:18080` returned 200 with the expected HTML; Chrome screenshot confirmed correct rendering (after the charset fix — see `6_Semblance/error.log`/`fix.log`).
- **Result:** ✅ Passed
- **Date Validated:** 2026-09-10

---

### Hypothesis 1: Zarf can package and deploy a workload on minikube with no custom Kubernetes tooling beyond `kubectl`/`zarf`
- **Original Assumption:** Zarf's own in-cluster registry is sufficient — no manual image push or external registry needed.
- **Validation Method:** Built and deployed a manifest-only package referencing a public image (`nginx:1.27-alpine`) and watched the deploy logs.
- **Evidence:** `zarf package deploy` log line `pushing image name=docker.io/library/nginx:1.27-alpine` — Zarf pushed it through `zarf-docker-registry` automatically.
- **Result:** ✅ Passed
- **Date Validated:** 2026-09-10

### Hypothesis 2: `zarf init` is safe to re-run / cheap to redo if the cluster is reset
- **Original Assumption:** Re-running `zarf init` on a fresh cluster fully restores the Zarf control plane without special cleanup.
- **Validation Method:** Not yet tested — would require tearing down and recreating minikube.
- **Evidence:** N/A
- **Result:** ⚠️ Partial (not yet exercised)
- **Date Validated:** —

### Hypothesis 3: RULE-005 is compatible with a real infrastructure PoC
- **Original Assumption:** The allowed-root-folders rule wouldn't need to be broken even once real tooling (Zarf/Docker/minikube) was involved.
- **Validation Method:** Tracked every point a tool wanted a root-level directory or file during this work.
- **Evidence:** One conflict found (`.devcontainer/`), resolved via ADR-002 in `4_Formula/decisions.md` (manual setup guide instead). Build artifacts routed to `~/.zarf-cache/` via `--output`, never touching the repo — confirmed by `smoke_test.py`'s Root Layout (RULE-005) check passing after every commit in this work.
- **Result:** ✅ Passed
- **Date Validated:** 2026-09-10

---

### Question: Does the Codespaces default machine size run minikube + Zarf init acceptably?
- **Original Question:** Is a bigger Codespaces machine type required?
- **Resolution:** Not yet answered — this PoC validated the workflow on a local macOS machine, not inside an actual Codespace. Tracked as Q1 in `1_Real_Unknown/questions.md` and R-001 in `1_Real_Unknown/risks.md`.
- **Linked Decision:** N/A — open
- **Result:** ⚠️ Open
- **Date Resolved:** —

---

## 🏁 Final Sign-off
- **Prepared By:** Claude (Test Agent)
- **Validation Date:** 2026-09-10
- **Overall Status:** 🟢 Go — both project OKRs achieved and verified locally; one open item (validating inside an actual Codespace, not just locally) carried forward as Q1/R-001.
- **Comments/Notes:** Smoke tests (`5_Symbols/toolbox/smoke_test.py`) pass 11/11 as of this report. See `6_Semblance/smoke_test_report.md` for the raw run.
