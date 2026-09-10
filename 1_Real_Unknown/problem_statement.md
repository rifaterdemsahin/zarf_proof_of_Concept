# 🎯 Problem Statement

> **Stage 1: Real Unknown** — Clearly define the pain point, gap, or opportunity before starting.

---

## 🔍 Core Problem / Pain Point
*Describe the primary problem you are trying to solve. What is broken, inefficient, or missing?*

- **Current State:** No hands-on experience with Zarf's air-gapped/private package system. It is unclear what Zarf actually provides (packaging format, `zarf init`, package registry/runtime) versus other Kubernetes packaging tools (Helm, Kustomize).
- **Ideal State:** A working Zarf install running inside a GitHub Codespaces minikube cluster, `zarf init` completed against the public init package, and a private Zarf package built and deployed that showcases a hello-world website.
- **The Gap:** No Zarf tooling installed, no Codespaces devcontainer configured for minikube + Zarf, and no private package definition (`zarf.yaml`) authored yet.

## 👥 Target Audience & Stakeholders
*Who is experiencing this pain point? Who will benefit from the solution?*

- **Primary User:** rifaterdemsahin — learning Zarf's packaging model for future air-gapped/offline Kubernetes delivery work.
- **Secondary Stakeholders:** Any future project that needs air-gapped or private-registry Kubernetes package delivery.

## 💡 Proposed Value Proposition
*How does solving this problem add value? What are the high-level benefits?*

- Demonstrates an end-to-end Zarf workflow (init → build → deploy) that can be reused as a reference for real air-gapped delivery projects.
- Produces a private Zarf package (hello-world website) as a concrete, showable artifact — proof the packaging system works, not just documentation.

## 🚀 Constraints & Scope Boundaries
*What is explicitly out of scope or a known constraint for this problem definition?*

- Environment is GitHub Codespaces only (not local Docker Desktop / not a bare-metal cluster) for this PoC.
- Scope is a single hello-world workload — not a production-grade multi-service package.
- No air-gapped network simulation in this PoC; the focus is the packaging/build/deploy workflow, not the offline transfer story.
