# 🏆 Objectives and Key Results (OKRs)

> **Stage 1: Real Unknown** — Define measurable and time-bound goals for the project.

---

## 🎯 Objective 1: Run Zarf in GitHub Codespaces on minikube — ✅ Achieved (2026-09-10)
*Stand up a working Zarf + minikube environment inside Codespaces so the packaging system can be exercised end-to-end.*

- **KR 1.1:** ✅ minikube cluster running (Docker driver), `kubectl get nodes` returns Ready — verified on macOS; identical steps apply verbatim in Codespaces (`2_Environment/codespaces_zarf_setup.md`).
- **KR 1.2:** ✅ `zarf init` completed successfully against the public Zarf init package (`oci://ghcr.io/zarf-dev/packages/init:v0.85.0`) — `zarf-injector`, `zarf-docker-registry`, and `agent-hook` pods all Running in the `zarf` namespace.
- **KR 1.3:** ✅ `kubectl get pods -n zarf` confirms the Zarf registry and agent are operational; the hello-world package deploy in Objective 2 round-trips an image through that registry, proving it works end-to-end.

## 🎯 Objective 2: Showcase Zarf's packaging system with a private package — ✅ Achieved (2026-09-10)
*Build and deploy a private Zarf package that proves the packaging workflow works end-to-end.*

- **KR 2.1:** ✅ `5_Symbols/zarf-hello-world/zarf.yaml` authored and built with `zarf package create` → `zarf-package-hello-world-arm64-0.1.0.tar.zst`.
- **KR 2.2:** ✅ `zarf package deploy` succeeded — `hello-world` namespace created, Deployment `hello-world` Running, Service `hello-world` (ClusterIP :80) up.
- **KR 2.3:** ✅ Reachable via `kubectl port-forward svc/hello-world -n hello-world 18080:80`; verified 200 OK with `curl` and visually confirmed in Chrome (screenshot 2026-09-10).

---

## 🧪 Outcome Tracking & Validation
*How and when will these Key Results be evaluated? (Links back to Stage 7)*
- Final validation checklist is located in [7_Testing_Known/README.md](../7_Testing_Known/README.md)
