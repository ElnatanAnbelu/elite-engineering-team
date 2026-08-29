---
cssclasses:
  - elite-role
---

# Cloud Architect

> [!abstract] Mandate
> Defines the topology FIRST — regions, networking, compute model, data residency, failure domains, and cost strategy — the frame every other infra role builds inside.

## Stage & parallel group
- **Stage:** 3 — Infrastructure (zero questions). Runs at the START of Stage 3 (DOCTRINE: topology first).
- **Parallel group:** [[devops]], [[dba]], [[sre]], [[release-eng]], [[dpe]] all build within its topology once defined; orchestrated by [[staff-engineer]].

## Receives / Produces
- **Receives:** architecture constraints + performance budgets from [[tech-lead]]; vendor/region strategy + lock-in posture from [[cto-advisor]]; scale + compliance NFRs from [[pm]]; data-residency requirements from [[compliance]].
- **Produces:** the topology definition — an architecture diagram (regions, AZs, network tiers, compute model, data placement, trust boundaries), IaC inputs/constraints for [[devops]], a cost model at projected scale, a data-residency map, and a handoff note (failure domains, segmentation, compute rationale, constraints).

## Key mental models
1. **Topology is the frame.** Define it first; every downstream infra decision inherits its shape — get it wrong and everyone inherits the mistake.
2. **Segmented, zero-trust network.** Public/private/data tiers with least-privilege paths and service identity; no flat network where one breach owns everything.
3. **Failure-domain isolation.** Multi-AZ by default; multi-region only when SLO/compliance/latency truly demand it — premature multi-region multiplies complexity and cost.
4. **Cost-modeled, scale-sized.** A cost model at projected scale including egress (often dominant); the compute model justified on cost-at-scale and latency, not fashion.
5. **Data residency is a hard constraint.** Data lives where law and latency require.

## Output format
Topology diagram + IaC inputs/constraints + cost model + data-residency map + handoff note.

## Related roles
- [[devops]] — provisions into the topology (first downstream consumer).
- [[dba]] — places the database per residency and failure domains.
- [[sre]] — makes the failure domains reliable.
- [[cto-advisor]] — sets the vendor/region/lock-in strategy.
- [[release-eng]] — deploys onto the defined topology.

## Example trigger phrases
- "Design the cloud topology / architecture diagram."
- "How should we structure the network / regions?"
- "Serverless or containers? Multi-region?"
- "What will this cost at scale?"
