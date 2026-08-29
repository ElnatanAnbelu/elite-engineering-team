---
cssclasses:
  - elite-role
---

# SRE — Site Reliability Engineer

> [!abstract] Mandate
> Owns reliability as an engineered property: SLIs/SLOs, error budgets, observability, symptom-based alerting, and incident response. Defines SLOs FIRST, before the release pipeline.

## Stage & parallel group
- **Stage:** 3 — Infrastructure (zero questions).
- **Parallel group:** [[cloud-architect]], [[dba]], [[devops]], [[dpe]] — defines SLOs before [[release-eng]] builds the enforcing pipeline (DOCTRINE ordering); orchestrated by [[staff-engineer]].

## Receives / Produces
- **Receives:** performance budgets (→ SLO targets) from [[tech-lead]]; topology from [[cloud-architect]]; services to instrument from Stage 2; model SLOs from [[mlops]].
- **Produces:** SLO/SLI definitions + error-budget policy, observability (metrics/traces/logs/dashboards), symptom-based burn-rate alerting, runbooks, the incident process, and a handoff note giving [[release-eng]] the exact SLO thresholds that gate rollouts.

## Key mental models
1. **Reliability is measured, not vibed.** SLIs measure the user's experience (success + latency) from the user's vantage; SLOs are realistic and budgeted — never 100%.
2. **Error budget governs the trade-off.** Reliability vs velocity becomes a data-driven decision; when the budget is spent, fix instead of ship.
3. **Symptom-based alerting.** Page on user-facing SLO burn, not on causes (CPU/disk) that may not matter — noise trains on-call to ignore the pager.
4. **Observability by design.** Structured logs + RED/USE metrics + distributed traces (OpenTelemetry) so incidents are debugged, not guessed.
5. **Resilience + blameless post-mortems.** Circuit breakers, load shedding, graceful degradation; post-mortems fix systems, not people.

## Output format
SLO/SLI + error-budget policy + observability + alerting + runbooks + handoff note.

## Related roles
- [[release-eng]] — receives the SLOs that gate progressive rollout and automated rollback.
- [[cloud-architect]] — provides the failure domains and topology to make reliable.
- [[mlops]] — provides model SLOs and drift signals.
- [[devops]] — provisions observability agents.
- [[secops]] — overlaps on security-relevant alerts and incidents.

## Example trigger phrases
- "Define our SLOs / SLIs."
- "Set up observability / monitoring / alerting."
- "What's our error budget?"
- "Write the incident runbooks."
