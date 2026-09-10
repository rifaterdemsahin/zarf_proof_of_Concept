# zarf-hello-world — Private Zarf Package

> **Stage 5: Symbols** — Source for the private Zarf package that showcases Zarf's packaging system (SPEC-014).

## Contents

- `zarf.yaml` — package definition: one component (`hello-world`) bundling an nginx image and a Kubernetes manifest.
- `manifests/hello-world.yaml` — Namespace, ConfigMap (static `index.html`), Deployment, and Service for the hello-world site.

## Build & Deploy

See [`2_Environment/codespaces_zarf_setup.md`](../../2_Environment/codespaces_zarf_setup.md) for the full Codespaces + minikube walkthrough. Short version, from this directory:

```bash
zarf package create . --confirm
zarf package deploy zarf-package-hello-world-*.tar.zst --confirm
kubectl port-forward svc/hello-world -n hello-world 8080:80
```
