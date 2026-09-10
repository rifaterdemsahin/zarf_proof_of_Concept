# Codespaces + minikube + Zarf Setup

> **Stage 2: Environment** — How to stand up Zarf on minikube inside a GitHub Codespace for this PoC.

## Why Codespaces (no `.devcontainer/`)

RULE-005 only allows these root folders: `.claude/skills`, `.github/workflows`, `.kilo/skills`, and the seven stage folders. A `.devcontainer/` directory is not on that list, so this project does **not** ship an auto-configuring devcontainer. Instead, a Codespace is opened on the default image and this guide is run manually (or pasted into a setup script kept in `5_Symbols/` and invoked from the Codespace terminal). This keeps the repo root compliant with RULE-005 while still working in Codespaces. See `4_Formula/decisions.md` for this trade-off.

## Prerequisites

- A GitHub Codespace opened on this repo (default machine type is fine to start; bump to 4-core/8GB if minikube is slow — see `1_Real_Unknown/risks.md` R-001).
- Docker is already available inside the Codespace image (used as the minikube driver).

## 1. Install the Zarf CLI

```bash
# Installs the latest Zarf CLI release for linux-amd64
curl -sL "https://get.zarf.dev" | bash
zarf version
```

## 2. Install / verify minikube and kubectl

```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube /usr/local/bin/minikube
minikube version

# kubectl is preinstalled on most Codespaces images; verify:
kubectl version --client
```

## 3. Start minikube

```bash
minikube start --driver=docker --cpus=4 --memory=6g
kubectl get nodes
```

## 4. Initialize Zarf against the public init package

```bash
zarf init --confirm
zarf tools kubectl get pods -n zarf
```

This pulls the public Zarf init package, installs the in-cluster Zarf registry/agent, and gets the cluster ready to receive Zarf packages.

## 5. Build and deploy the private hello-world package

The package definition lives in [`5_Symbols/zarf-hello-world/`](../5_Symbols/zarf-hello-world/).

```bash
cd 5_Symbols/zarf-hello-world
zarf package create . --confirm
zarf package deploy zarf-package-hello-world-*.tar.zst --confirm
```

## 6. View the hello-world site

```bash
kubectl port-forward svc/hello-world -n hello-world 8080:80
# open http://localhost:8080 (Codespaces will offer to forward the port)
```

## Related

- [`architecture.md`](architecture.md) — where this fits in the overall system
- [`dependencies.md`](dependencies.md) — Zarf CLI / minikube / kubectl version pins
- [`4_Formula/specs.md`](../4_Formula/specs.md) — SPEC for the private Zarf package
- [`1_Real_Unknown/okrs.md`](../1_Real_Unknown/okrs.md) — Objective 1 & 2 this setup satisfies
