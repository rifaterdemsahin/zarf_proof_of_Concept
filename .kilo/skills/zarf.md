# Zarf Packaging Skill

Load this skill when working with Zarf, minikube, or the private `hello-world` package in this project.

## Purpose

Guide building, deploying, and troubleshooting Zarf packages against the Codespaces minikube cluster for this PoC (`1_Real_Unknown/okrs.md`).

## Core Workflow

1. **Environment** — follow [`2_Environment/codespaces_zarf_setup.md`](../../2_Environment/codespaces_zarf_setup.md): install Zarf CLI + minikube, start the cluster, `zarf init --confirm`.
2. **Package source** — package definitions live under `5_Symbols/<package-name>/` as `zarf.yaml` + `manifests/`. Never put Zarf packages outside `5_Symbols/` (RULE-005).
3. **Build**: `zarf package create <dir> --confirm` — produces a `.tar.zst` archive.
4. **Deploy**: `zarf package deploy <archive> --confirm`.
5. **Verify**: `kubectl get pods -n <namespace>` then `kubectl port-forward svc/<name> -n <namespace> <local>:<remote>`.

## Zarf Concepts (quick reference)

- `zarf init` — bootstraps the in-cluster Zarf registry/agent using the **public** Zarf init package; required once per cluster before any package deploy.
- A **Zarf package** (`zarf.yaml`) bundles Kubernetes manifests/Helm charts + the container images they reference into one distributable artifact — this is what makes it usable air-gapped.
- `components[].manifests` — raw Kubernetes YAML to apply; `components[].charts` — Helm charts; `components[].images` — images Zarf must pull and re-host through its registry.
- Private packages (like `5_Symbols/zarf-hello-world`) don't need to be published anywhere public — they're built and deployed directly from the local `.tar.zst`.

## Rules

- Never hardcode registry credentials in `zarf.yaml` — pull from Azure Key Vault per RULE-003/004 if a private registry is later added.
- After any package change, update the SPEC in `4_Formula/specs.md` describing the package **as delivered** (RULE-001), then commit and push (RULE-002).
- Record any Zarf/minikube resource issues in `1_Real_Unknown/risks.md` (see R-001) and errors in `6_Semblance/error.log`.

## Troubleshooting

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| `zarf init` hangs | minikube under-resourced | Restart with more CPU/memory (see R-001) |
| `zarf init --confirm` errors "requires a zarf-init package... re-run without --confirm" | Non-interactive `--confirm` can't answer the download-consent prompt | `zarf package pull oci://ghcr.io/zarf-dev/packages/init:<version>` first, then `zarf init <local-tarball-path> --confirm` (positional arg, not a flag) |
| `zarf package deploy` fails pulling image | Image not listed under `components[].images` | Add the image reference to `zarf.yaml` |
| Pod stuck `ImagePullBackOff` after deploy | Zarf registry not reachable from the pod | `zarf tools kubectl get pods -n zarf`; re-run `zarf init` |
| Redeployed pod's changes don't show up in the browser | An existing `kubectl port-forward` is still proxying to the old (replaced) pod | Kill and restart the port-forward after every redeploy |
| Pulled/built `.tar.zst` package lands in the repo root | Zarf CLI defaults to writing to the current directory | `zarf package create . --output ~/.zarf-cache/` (or any path outside the repo) — never commit build artifacts (RULE-005) |
