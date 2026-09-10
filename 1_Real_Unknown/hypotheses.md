# 🧪 Hypotheses

> **Stage 1: Real Unknown** — Document your initial assumptions and how they will be validated in Stage 7.

---

## 🔍 Core Hypotheses

### Hypothesis 1: Zarf can package and deploy a workload on minikube with no custom Kubernetes tooling beyond `kubectl`/`zarf`
*A `zarf.yaml` + plain manifests package should build, deploy, and run without needing Helm charts, an external registry, or manual image pushes — Zarf's own in-cluster registry should be enough.*

- **Rationale:** Zarf's core value proposition is "self-contained, air-gap-ready packages" — if it still requires external registry setup for a trivial hello-world, the packaging story is weaker than advertised.
- **Validation Method:** Build (`zarf package create`) and deploy (`zarf package deploy`) a manifest-only package and confirm the pod comes up without any manual `docker push` or registry configuration.
- **Linked Test:** [7_Testing_Known/validation_report.md](../7_Testing_Known/validation_report.md)
- **Status:** ✅ **Confirmed (2026-09-10)** — `zarf package deploy` pushed the `nginx:1.27-alpine` image through the in-cluster `zarf-docker-registry` automatically; no manual registry steps were needed.

---

### Hypothesis 2: `zarf init` is safe to re-run / cheap to redo if the cluster is reset
*If minikube gets torn down and recreated (e.g. a fresh Codespace), re-running `zarf init` should fully restore the Zarf control plane without special cleanup.*

- **Rationale:** Codespaces environments are ephemeral by default — a workflow that requires manual cleanup before re-init would be fragile for this PoC's stated environment.
- **Validation Method:** Not yet tested — would require tearing down and recreating the minikube cluster, then re-running `zarf init`.
- **Linked Test:** [7_Testing_Known/validation_report.md](../7_Testing_Known/validation_report.md)
- **Status:** ⏳ Pending Validation

---

### Hypothesis 3: RULE-005 (allowed root folders only) is compatible with a real infrastructure PoC, not just documentation-only projects
*The framework's root-folder restriction was designed around a docs/website template; this hypothesis is whether it still holds up once real build tooling (Zarf, Docker, minikube) enters the picture.*

- **Rationale:** Real tools often want their own root-level config/cache directories (e.g. `.devcontainer/`); if RULE-005 can't accommodate that without workarounds, it may need revisiting for infra-heavy projects.
- **Validation Method:** Track every point where a tool "wants" a root directory and record how it was resolved (see ADR-002 in `4_Formula/decisions.md`).
- **Linked Test:** [7_Testing_Known/validation_report.md](../7_Testing_Known/validation_report.md)
- **Status:** ✅ **Confirmed workable (2026-09-10)** — one conflict found (`.devcontainer/`), resolved by keeping Zarf/minikube setup as a documented manual guide instead of an auto-configuring devcontainer. Build artifacts (`.tar.zst` packages) were also kept out of the repo via `--output` flags rather than needing a new gitignored root folder.
