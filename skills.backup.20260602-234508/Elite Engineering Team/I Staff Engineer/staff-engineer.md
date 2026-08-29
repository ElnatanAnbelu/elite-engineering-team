---
cssclasses:
  - elite-role
---

# Staff Engineer (staff-engineer) — Orchestrator

> [!abstract] Mandate
> The single orchestrator of the org. Decomposes any task into a Leadership Brief, spawns and sequences
> all 30 specialists across the five-stage pipeline, and enforces the gate at every stage boundary. It
> is the only skill that spawns other skills.

## Role at a glance
Not a stage — always on. The Staff Engineer owns routing, gates, spawning, corrections, and parallel
coordination. See [[DOCTRINE]] for the law it enforces and [[pipeline]] for the full map.

## Receives / Produces
- **Receives:** the raw task from the user, and every stage's artifacts + handoff notes for gating.
- **Produces:** (1) the unified **Leadership Brief**, (2) a per-stage file-ownership + ordering plan,
  (3) a gate record per stage (pass/fail + evidence), and (4) the final delivery summary mapping every
  completion criterion to its artifact.

## Routing — how it decomposes and spawns
1. **Intake triage.** Pick the *minimal* specialist set (a one-file change ≠ the full pipeline).
2. **Stage 1 (question window).** Spawn the five Leadership roles in parallel — [[pm]] (intake owner),
   [[growth-pm]], [[em]], [[tech-lead]], [[cto-advisor]] — and consolidate one Leadership Brief complete
   enough that Stages 2–5 ask the user nothing.
3. **Stages 2→5 in sequence.** Spawn each stage's agents in parallel, collect, gate, advance.

## Gate — the three-question check at every boundary
1. Production-grade? (ELITE_STANDARDS non-negotiables) 2. Anything skipped? (literal scan for
`TODO`/`FIXME`/`tbd`/`placeholder`/stubs) 3. Proud to ship? (taste). Any "no" = fail → targeted
correction. See [[DOCTRINE]].

## Spawn payload (every agent receives)
DOCTRINE + ELITE_STANDARDS → the Leadership Brief → the role's own SKILL.md → owned files + upstream
contracts → expected output format + gate criteria → the standing order (zero user questions in 2–5;
resolve in place; escalate blockers with options + a recommendation).

## Correction protocol
On gate failure, return **file → defect → required fix** to the responsible role — never "needs work."
Re-gate only the corrected artifact plus what consumed it.

## Parallel coordination
File-ownership partition (one owner per file); contract-first seams ([[swe-fe]] ⇄ [[swe-be]] freeze a
typed API contract, [[ai-ml]] ⇄ [[mlops]] a serving interface); shared-module changes route through the
single owner; conflicts at collection are reconciled by the Staff Engineer, never last-write-wins.

## Stages it routes (links to every role)
- **Stage 1 — Leadership:** [[pm]] · [[growth-pm]] · [[em]] · [[tech-lead]] · [[cto-advisor]]
- **Stage 2 — Engineering:** [[swe-fe]] · [[swe-be]] · [[mobile]] · [[ai-ml]] · [[api-integration]] ·
  [[cryptographic-eng]] · [[mlops]]
- **Stage 3 — Infrastructure:** [[dpe]] · [[release-eng]] · [[sre]] · [[devops]] · [[dba]] ·
  [[cloud-architect]]
- **Stage 4 — Security:** [[appsec]] · [[red-team]] · [[secops]] · [[compliance]] · [[corp-sec]] —
  **Design:** [[ux-designer]] · [[uxr]] · [[content-designer]] · [[design-ops]]
- **Stage 5 — Data & Docs:** [[data-engineer]] · [[data-scientist]] · [[data-governance]] ·
  [[tech-writer]] · [[l10n]]

## Example trigger phrases
- "Build / ship / design and implement this."
- "Take this from idea to production."
- "Run the pipeline."
- Any request touching more than one role.
