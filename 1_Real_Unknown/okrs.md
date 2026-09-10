# 🏆 Objectives and Key Results (OKRs)

> **Stage 1: Real Unknown** — Define measurable and time-bound goals for the project.

---

## 🎯 Objective 1: Run Zarf in GitHub Codespaces on minikube
*Stand up a working Zarf + minikube environment inside Codespaces so the packaging system can be exercised end-to-end.*

- **KR 1.1:** minikube cluster is running inside a Codespace and `kubectl get nodes` returns Ready.
- **KR 1.2:** `zarf init` completes successfully against the public Zarf init package.
- **KR 1.3:** `zarf tools` / `zarf package list` commands work against the cluster, confirming the Zarf registry and agent are operational.

## 🎯 Objective 2: Showcase Zarf's packaging system with a private package
*Build and deploy a private Zarf package that proves the packaging workflow works end-to-end.*

- **KR 2.1:** A custom `zarf.yaml` package is authored and built (`zarf package create`) containing a hello-world website.
- **KR 2.2:** The private package deploys successfully (`zarf package deploy`) into the Codespaces minikube cluster.
- **KR 2.3:** The hello-world website is reachable (via `kubectl port-forward` or minikube service URL) and demonstrable to others.

---

## 🧪 Outcome Tracking & Validation
*How and when will these Key Results be evaluated? (Links back to Stage 7)*
- Final validation checklist is located in [7_Testing_Known/README.md](../7_Testing_Known/README.md)
