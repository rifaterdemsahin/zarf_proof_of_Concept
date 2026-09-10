# Logic Tracker — Premise & Conclusion

> Managed by the **Test Agent**. Tracks the premise→conclusion chain across objectives, delivered tasks, and LLM decisions.

## Format

| # | Premise | Objective | Task Delivered | LLM Decision | Conclusion | Status |
|---|---------|-----------|----------------|--------------|------------|--------|
|   |         |           |                |              |            |        |

## Structure

- **Premise**: The starting assumption, requirement, or question
- **Objective**: The OKR or goal this maps to
- **Task Delivered**: The concrete task or PR that addressed it
- **LLM Decision**: Key choice the LLM made (model selection, architecture, trade-off)
- **Conclusion**: Whether the premise holds, was disproven, or needs iteration
- **Status**: ✅ Confirmed / ❌ Rejected / 🔄 Iterating

## Iteration

When a conclusion is `🔄 Iterating`, the next row continues with the updated premise.

---

## Entries

| # | Premise | Objective | Task Delivered | LLM Decision | Conclusion | Status |
|---|---------|-----------|----------------|--------------|------------|--------|
| 1 | Agents forget to spec delivered work and leave changes unpushed | Template agents share one standing-orders file | TSK-027 / SPEC-011 — `5_Symbols/rules/agent_operating_rules.md` | Put RULE-001 (spec as delivered into Formula) and RULE-002 (commit and push) in `5_Symbols/rules/`, pointed from `agents.md` | Premise holds: one loadable file + Formula spec of the work | ✅ Confirmed |
| 2 | Backend host and default storage must be explicit for agents | RULE-003/004 so backends land on Fly.io or Workers with Key Vault creds; blobs on Azure | TSK-028 / SPEC-012 | Workers for light/stateless; Fly.io for heavy containers; Azure project storage as default blobs | Premise holds: standing orders + architecture + tools aligned | ✅ Confirmed |
| 3 | Root must not accumulate stray folders | RULE-005: only stage + skill/workflow dirs at root; move extras | TSK-029 / SPEC-013 | Keep Pages/git/coordinator files at root; move everything else into the matching allowed folder | Premise holds: placement map + file_organization aligned | ✅ Confirmed |
| 4 | Zarf can package/deploy a workload on minikube using only its own in-cluster registry, no external registry setup | Objective 2 (`okrs.md`) — showcase the packaging system with a private package | TSK-008–012, SPEC-014 — `5_Symbols/zarf-hello-world/` | Build a manifest-only package referencing a public image; let `zarf package deploy` push it through `zarf-docker-registry` | Premise holds: deploy succeeded with zero manual registry steps | ✅ Confirmed |
| 5 | RULE-005 (allowed root folders) would need to be broken once real infra tooling (Zarf/Docker/minikube) enters the project | Objective 1 (`okrs.md`) — run Zarf in Codespaces minikube | ADR-002 in `4_Formula/decisions.md`, `2_Environment/codespaces_zarf_setup.md` | Skip a root `.devcontainer/`; document manual setup instead; route all build artifacts (`.tar.zst`) to `~/.zarf-cache/` outside the repo via `--output` | Premise disproven — RULE-005 held with no exceptions needed, only workflow adjustments | ❌ Rejected (premise), i.e. the framework rule survived intact |
| 6 | `curl`/`kubectl get` status checks are sufficient to verify a deployed website works | Objective 2 (`okrs.md`) — hello-world site reachable and demonstrable | TSK-013 — Chrome screenshot verification | Take an actual browser screenshot instead of stopping at `curl` 200 OK | Premise disproven: `curl` missed a real rendering bug (`&#128075;` mojibake from missing `<meta charset>`), only found by looking at rendered output | ❌ Rejected — visual verification is now the standard for TSK-013-type checks |
