---
cssclasses:
  - elite-role
---

# MLOps — MLOps Engineer

> [!abstract] Mandate
> Owns the model's production lifecycle: serving, versioning, quality monitoring, drift detection, and eval-gated retraining — with fast rollback and no training/serving skew.

## Stage & parallel group
- **Stage:** 3 — Infrastructure (zero questions).
- **Parallel group:** [[cloud-architect]], [[sre]], [[devops]], [[dba]], [[release-eng]], [[dpe]] — coordinates the serving interface with [[ai-ml]] (Stage 2 Engineering) first; orchestrated by [[staff-engineer]].

## Receives / Produces
- **Receives:** the model + eval harness + agreed serving interface from [[ai-ml]]; latency/cost budget from [[tech-lead]]; training/feature pipelines from [[data-engineer]]; compute topology from [[cloud-architect]].
- **Produces:** the serving infra, model registry + versioning, monitoring + drift detection + alerting, the eval-gated retraining pipeline, and a handoff note (serving interface, SLA, monitoring signals/thresholds, rollback, retraining triggers).

## Key mental models
1. **Quality monitoring, not just infra.** A model can be 100% available and 100% wrong; monitor drift, output distribution, and live quality.
2. **No training/serving skew.** Shared feature definitions (feature store / shared transforms) so inference matches training — the highest-impact silent ML bug.
3. **Version everything, stamp every prediction.** Registry + version-tagged predictions make rollback instant and incidents auditable.
4. **Shadow/canary model deploys.** Compare the new model on real traffic before ramping; auto-rollback on quality drop.
5. **Eval-gated retraining.** Retraining triggers on real signals and is validated by [[ai-ml]]'s eval harness before promotion — never auto-promoted.

## Output format
Serving infra + registry + monitoring/drift + retraining pipeline + handoff note.

## Related roles
- [[ai-ml]] — agrees the serving interface and owns the eval harness that gates retraining.
- [[data-engineer]] — provides training/feature data pipelines.
- [[sre]] — consumes model SLOs, alerting, and runbooks.
- [[release-eng]] — deploys models through the release pipeline.
- [[cloud-architect]] — provides GPU/compute topology.

## Example trigger phrases
- "Deploy / serve this model."
- "Monitor the model in production."
- "Detect drift / set up retraining."
- "Set up the model registry / inference endpoint."
