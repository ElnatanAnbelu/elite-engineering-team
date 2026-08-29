---
cssclasses:
  - elite-doc
---

# DOCTRINE (vault companion)

> The Obsidian companion to `skills/DOCTRINE.md` — the master law of the org. This note summarizes the
> law and links every role. The authoritative source is the root `DOCTRINE.md`; this is the navigable
> map. See also [[pipeline]] (the diagram) and [[staff-engineer|Staff
> Engineer]] (the enforcer).

## The three rules
1. **No skipping.** Every issue resolved in place — no TODOs, no placeholders, no "handle this later." A
   deliverable is the whole thing working end to end.
2. **Questions only in Stage 1.** Leadership is the only stage that asks the user anything. Stages 2–5
   execute from the Leadership Brief with zero questions (the sole exception: a genuine credential /
   private-fact blocker, which is flagged, worked around, and escalated — never forwarded to the user).
3. **No stopping until done.** Production-grade or it does not leave the system.

## The stage gate protocol
Stages are **sequential**; agents **within** a stage run in **parallel**. At every boundary the
[[staff-engineer|Staff Engineer]] checks exactly three things:
1. **Production-grade?** (ELITE_STANDARDS non-negotiables: typed, validated input, no silent failures,
   no hardcoded secrets, observable, no N+1, documented interfaces.)
2. **Anything skipped?** (Literal scan: zero `TODO`, `FIXME`, `tbd`, `placeholder`, `XXX`, or stubbed
   bodies.)
3. **Proud to ship?** (The taste check — a principal engineer would ship it unchanged.)
Any "no" fails the gate → a **targeted correction** (file → defect → fix) returns to the responsible
role. The gate does not pass until all three are "yes."

## The question window (Stage 1 only)
```
Task In → STAGE 1 (questions) → [G1] → STAGE 2 → [G2] → STAGE 3 → [G3]
        → STAGE 4 → [G4] → STAGE 5 → [final gate] → Delivered
```
[[pm|PM]] runs intake covering: what is built and for whom; success criteria; technical
constraints and existing systems; non-functional requirements (scale, latency, regions, compliance);
and anything only the user knows. If a downstream stage ever wants to ask the user something, that is a
Stage 1 defect — routed back to Leadership, not to the user.

## Parallel vs sequential rules
- **Across stages: sequential** — Stage N+1 never starts before Stage N passes its gate.
- **Within a stage: parallel** — with these ordering constraints enforced even while parallel:
  - **Stage 1:** the Leadership intake runs in parallel; the Discovery cluster flows
    [[ux-designer|UX]] → [[uxr|UXR]] → [[content-designer|Content]] →
    [[design-ops|Design Ops]] off the same brief.
  - **Stage 2:** [[cryptographic-eng|Crypto]] consulted before auth/token code;
    [[swe-fe|FE]] ⇄ [[swe-be|BE]] freeze the API contract before
    implementing; [[mobile|Mobile]] uses the same contract;
    [[ai-ml|AI/ML]] defines the serving interface for [[mlops|MLOps]] (Stage 3) first.
  - **Stage 3:** [[cloud-architect|Cloud Architect]] defines topology first;
    [[sre|SRE]] sets SLOs before [[release-eng|Release Eng]] builds
    the pipeline; [[dba|DBA]] owns all migrations; [[mlops|MLOps]] consumes
    [[ai-ml|AI/ML]]'s serving interface.
  - **Stage 4:** Security flows [[appsec|AppSec]] → [[red-team|Red Team]] →
    [[secops|SecOps]], with [[compliance|Compliance]] +
    [[corp-sec|Corp Security]] in parallel; [[qa-engineer|QA Engineer]] runs the
    independent quality audit alongside.
  - **Stage 5:** [[data-engineer|Data Engineer]] builds pipelines before
    [[data-scientist|Data Scientist]] analyzes; [[data-governance|Data Governance]]
    governs throughout; [[tech-writer|Tech Writer]] documents every surface;
    [[l10n|L10n]] reviews all user-facing copy.
- **Write-conflict rule:** two agents never write the same file; the Staff Engineer partitions files by
  owner before spawning.

## The full 33-skill roster by stage
**Orchestrator (always on):** [[staff-engineer|Staff Engineer]].

**Stage 1 — Leadership + Discovery** *(question window; output = Leadership Brief — includes the Discovery cluster)*
[[pm|PM]] · [[growth-pm|Growth PM]] · [[em|EM]] ·
[[tech-lead|Tech Lead]] · [[cto-advisor|CTO Advisor]] ·
[[ux-designer|UX Designer]] · [[uxr|UXR]] ·
[[content-designer|Content Designer]] · [[design-ops|Design Ops]]

**Stage 2 — Engineering**
[[swe-fe|SWE-FE]] · [[swe-be|SWE-BE]] · [[mobile|Mobile]] ·
[[ai-ml|AI/ML]] · [[api-integration|API Integration]] ·
[[cryptographic-eng|Cryptographic Eng]]

**Stage 3 — Infrastructure**
[[dpe|DPE]] · [[release-eng|Release Eng]] ·
[[sre|SRE]] · [[devops|DevOps]] · [[dba|DBA]] ·
[[cloud-architect|Cloud Architect]] · [[mlops|MLOps]]

**Stage 4 — Security + QA** *(Security cluster + independent quality gate; one Sign-off Document)*
Security: [[appsec|AppSec]] · [[red-team|Red Team]] ·
[[secops|SecOps]] · [[compliance|Compliance]] ·
[[corp-sec|Corp Security]] — QA: [[qa-engineer|QA Engineer]]

**Stage 5 — Data & Docs**
[[data-scientist|Data Scientist]] · [[data-engineer|Data Engineer]] ·
[[data-governance|Data Governance]] · [[tech-writer|Tech Writer]] ·
[[l10n|L10n Specialist]]

> Counting note: **33 specialist skills + the Staff Engineer orchestrator.** The numbering reflects
> pipeline position, not extra specialists. The law lives in `skills/DOCTRINE.md`; the bar lives in
> `skills/ELITE_STANDARDS.md`; the [[staff-engineer|Staff Engineer]] enforces both.
