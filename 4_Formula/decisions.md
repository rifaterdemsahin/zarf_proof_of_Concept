# 🏛️ Architecture Decision Records (ADRs)

> **Stage 4: Formula** — Documenting major architectural decisions, their context, and consequences.

---

## 📋 ADR Index

- **ADR 001:** Choice of Secrets Manager (Azure Key Vault)
- **ADR 002:** No `.devcontainer/` — manual Codespaces setup script instead

---

## 📌 ADR 001: Choice of Secrets Manager (Azure Key Vault)

### **Status:** Accepted
**Date:** YYYY-MM-DD  
**Decided By:** [Human / AI Agent]

### **Context & Problem Statement**
*What is the context of this decision? What problem are we solving? (e.g. "We need a secure way to manage database credentials and API keys across environments without committing them to git.")*

### **Decision Drivers**
1. Zero secrets committed to version control.
2. Low cost for development operations.
3. Ease of integration with GitHub Actions and deployment platforms.

### **Considered Options**
- **Option 1:** Local `.env` files (Committed, high-risk).
- **Option 2:** Vault by HashiCorp (High configuration complexity, higher cost).
- **Option 3:** Azure Key Vault (FIPS compliance, pay-per-operation pricing).

### **Decision Outcome**
**Chosen Option:** **Option 3 (Azure Key Vault)**.
- **Why:** Fits enterprise-grade requirements, costs ~$0.03 per 10K requests (Standard tier), and interfaces natively with cloud pipelines.

### **Consequences**
- **Pros:** High security, audit logging, simple credential rotation.
- **Cons:** Requires active Azure credentials during CLI initialization and deployment pipelines.

---

## 📌 ADR 002: No `.devcontainer/` — manual Codespaces setup script instead

### **Status:** Accepted
**Date:** 2026-09-10
**Decided By:** AI Agent (Real Agent, per RULE-005)

### **Context & Problem Statement**
The project objective requires running Zarf on minikube inside GitHub Codespaces. Codespaces conventionally auto-configures via a `.devcontainer/devcontainer.json` at the repo root. RULE-005 restricts root folders to `.claude/skills`, `.github/workflows`, `.kilo/skills`, and the seven stage folders — `.devcontainer/` is not on that list.

### **Decision Drivers**
1. RULE-005 must not be silently violated for convenience.
2. The objective only needs a working Zarf + minikube environment, not a fully automated Codespace bootstrap.

### **Considered Options**
- **Option 1:** Add `.devcontainer/devcontainer.json` at the repo root (violates RULE-005).
- **Option 2:** Document a manual setup guide run from a default Codespace, with the steps recorded in `2_Environment/codespaces_zarf_setup.md`.

### **Decision Outcome**
**Chosen Option:** **Option 2** — manual setup guide, no root `.devcontainer/`.
- **Why:** Keeps the repo root within the allowed RULE-005 folder set; the PoC objective (see `1_Real_Unknown/okrs.md`) does not require zero-touch Codespace bootstrap.

### **Consequences**
- **Pros:** RULE-005 compliant; setup steps are explicit and versioned in `2_Environment/`.
- **Cons:** Opening a fresh Codespace requires manually running the setup steps (or a helper script in `5_Symbols/`) instead of it happening automatically on Codespace creation.
