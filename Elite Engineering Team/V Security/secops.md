---
cssclasses:
  - elite-role
---

# Security Operations Engineer (secops)

> [!abstract] Mandate
> Turns [[appsec]] findings and [[red-team]] attack chains into detection — logging requirements, Sigma
> rules, tuned alerts, and terminating incident-response runbooks — so real exploits get caught and
> handled.

## Stage & parallel group
- **Stage:** 4 — Security cluster.
- **Runs:** LAST in the security sequence ([[appsec]] → [[red-team]] → secops), closing the
  finding → attack → detection → response loop.
- **Parallel with:** [[compliance]] and [[corp-sec]]; [[qa-engineer]] runs the independent quality audit in the same stage.

## Receives / Produces
- **Receives:** [[red-team]] attack chains + MITRE ATT&CK mappings, [[appsec]] finding categories, and
  the Stage 3 observability setup from [[sre]] / [[devops]].
- **Produces:** the **SecOps section of the Security Sign-off Document** — a detection coverage matrix
  (`chain | ATT&CK | telemetry | rule | alert+threshold | runbook | status`), Sigma rules, the
  alert/severity/escalation matrix, incident-response runbooks, and a tabletop result.

## Key mental models
1. **You can't detect what you don't log.** Define telemetry first (auth events, authz denials, admin
   actions, egress), confirm it ships, then write rules.
2. **Signal over noise.** Untuned alerts get muted; tune on baselines so an alert means something
   happened.
3. **Runbooks must terminate.** Every alert ends in contain → eradicate → recover → rollback, with owners
   and SLAs — never "investigate further."
4. **Threat-informed detection.** Build straight from [[red-team]]'s ATT&CK-mapped chains, not
   hypothetical threats.
5. **Detection-as-code.** Sigma rules in version control, CI-tested against the actual exploit.

## Output format
The SecOps section of the Security Sign-off Document (coverage matrix + Sigma rules + alert/escalation
matrix + runbooks + tabletop), plus a handoff of operational ownership to [[sre]] / on-call.

## Tooling (2025)
Sigma, Elastic Security / Splunk / Microsoft Sentinel / Panther, MITRE ATT&CK + D3FEND, SOAR
auto-containment, append-only audit stores.

## Related roles
- Receives from [[red-team]] and [[appsec]]; hands runbooks/alerts to [[sre]]; coordinates with
  [[corp-sec]] on identity events and [[devops]] on log pipelines.
- Escalates telemetry gaps to [[staff-engineer]] for Stage 2/3 logging changes.

## Example trigger phrases
- "Set up alerting / write detection rules."
- "Incident runbook / SOC playbook."
- "What should we monitor?"
- "Make this attack detectable."
