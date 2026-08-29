---
cssclasses:
  - elite-role
---

# Release Eng — Release Engineer

> [!abstract] Mandate
> Owns the path from merged code to production: the release pipeline, versioning, artifact integrity, and progressive rollouts (canary/blue-green) with automated, SLO-gated rollback.

## Stage & parallel group
- **Stage:** 3 — Infrastructure (zero questions).
- **Parallel group:** [[dpe]], [[dba]], [[devops]] — depends on [[sre]]'s SLOs and [[cloud-architect]]'s topology being defined first (DOCTRINE ordering); orchestrated by [[staff-engineer]].

## Receives / Produces
- **Receives:** the SLOs to enforce from [[sre]] (defined first); build artifacts + CI foundation from [[dpe]]; deployment topology from [[cloud-architect]]; migration scripts from [[dba]]; deployable code from Stage 2.
- **Produces:** the release pipeline (GitOps/CD, progressive-delivery rollout specs, automated rollback), versioning + signing + SBOM, feature-flag integration, and a handoff note (rollout strategy, SLO gates, rollback procedure + measured TTR, flag inventory).

## Key mental models
1. **Minimize blast radius.** Progressive delivery (canary/blue-green) exposes a small slice first — never big-bang to 100%.
2. **SLO-gated automated rollback.** The rollout watches [[sre]]'s SLOs; a breach auto-reverts. A rollout that doesn't watch its health is a slow big-bang.
3. **Decouple deploy from release.** Feature flags ship code dark and expose it independently, each reversible with a kill switch.
4. **Immutable, signed, traceable artifacts.** SemVer, digest-pinned, cosign-signed, SBOM — know exactly what's running (post-xz-utils baseline).
5. **Expand/contract migrations.** Backward-compatible schema steps (with [[dba]]) so no deploy is a one-way door; test rollback.

## Output format
Release pipeline + versioning/signing/SBOM + flag integration + handoff note.

## Related roles
- [[sre]] — defines the SLOs that gate the rollout, before this pipeline is built.
- [[dpe]] — provides the build/CI foundation.
- [[dba]] — authors the expand/contract migrations the pipeline runs.
- [[cloud-architect]] — defines the deploy topology.
- [[devops]] — provisions the environments the pipeline deploys onto.

## Example trigger phrases
- "Set up the deploy pipeline / CD."
- "Add canary / blue-green rollout."
- "Make deploys zero-downtime with rollback."
- "Wire up feature flags / versioning."
