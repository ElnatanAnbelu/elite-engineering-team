# Master Build Brief — AI Engineering Skill Team
> Version 2.0 — Final approved brief. Hand this entire document to Claude Code.
> It contains everything needed to build the full project completely.

---

## What You Are Building

A fully operational AI engineering org built as Claude Code skills — 30 specialist skills + 1 orchestrator (Staff Engineer) + 3 foundation documents (DOCTRINE.md, ELITE_STANDARDS.md, ELITE_STANDARDS is pre-written) + a complete Obsidian knowledge vault. This is a commercial product sold as a $39 one-time purchase with an optional $5-7/month update subscription.

**Total files to build: 36 skill files + Obsidian vault = 70+ files.**

---

## Execution Rules

**Rule 1 — No skipping.** Every issue resolved in place before moving forward. No TODOs. No placeholders. No "handle this later."

**Rule 2 — Questions only in Stage 1.** Stage 1 Leadership agents ask questions to extract everything they need. Stages 2–5 receive the Leadership brief and execute with zero questions. The only exception in Stages 2–5: if you physically cannot proceed without a credential or private user info — flag it, work around everything else, and continue.

**Rule 3 — No stopping until done.** A task is complete when the entire deliverable works end to end. Not a draft, not a starting point — fully working.

**Rule 4 — Research before writing.** Before writing any skill file, run the mandatory research phase for that role. See Research Phase section below.

---

## Pipeline Architecture

Stages are sequential. A stage only begins when the previous stage is fully complete and has passed the Staff Engineer review gate. Within each stage, all agents run in parallel.

```
Task In
   ↓
STAGE 1 — Leadership
   PM · Growth PM · EM · Tech Lead · CTO Advisor
   [ONLY stage that asks questions — extracts everything all downstream stages need]
   ↓ [Staff Engineer gate]
STAGE 2 — Engineering
   SWE-FE · SWE-BE · Mobile · AI/ML · API Integration · Cryptographic Eng · MLOps
   [Zero questions — executes from Leadership brief alone]
   ↓ [Staff Engineer gate]
STAGE 3 — Infrastructure
   DPE · Release Eng · SRE · DevOps · DBA · Cloud Architect
   [Zero questions]
   ↓ [Staff Engineer gate]
STAGE 4 — Security + Design (parallel clusters)
   Security: AppSec · Red Team · SecOps · Compliance · Corp Security
   Design: UX Designer · UXR · Content Designer · Design Ops
   [Zero questions]
   ↓ [Staff Engineer gate]
STAGE 5 — Data & Docs
   Data Scientist · Data Engineer · Data Governance · Tech Writer · L10n Specialist
   [Zero questions]
   ↓ [Final Staff Engineer review gate]
Delivered — complete, production-grade, nothing skipped
```

**Stage 1 question window:** PM runs structured intake interview. All five Leadership agents contribute. They produce one unified Leadership Brief thorough enough that Stages 2–5 never need to ask the user anything.

**Stage gate logic:** Staff Engineer checks three things at every gate:
1. Is every output production-grade?
2. Is anything skipped, deferred, or left as a TODO?
3. Would a senior engineer at a top-tier company be proud to ship this?

If any answer is no — goes back to the responsible skill with specific corrections. Gate does not pass until all three are yes.

---

## Complete File Structure

Build everything at this exact path. Do not deviate.

> ⚠️ **CRITICAL — Flat skill structure (do not nest under category folders).**
> Claude Code only registers a personal/project skill when its `SKILL.md` sits **exactly one level deep**: `skills/<role>/SKILL.md`. If you nest by category — `skills/engineering/swe-be/SKILL.md` — Claude Code will **not** register the skill, and the user has to manually flatten it after install. Build flat from the start.
>
> Categories below (Leadership, Engineering, etc.) are **logical groupings for humans only** — they are NOT directories in `skills/`. Every role folder is a direct child of `skills/`. The `OBSIDIAN-VAULT/` keeps its numbered category subfolders because the vault is reference documentation, not registered skills.

```
skills/
├── DOCTRINE.md                          ← Build first (lives in skills/ root)
├── ELITE_STANDARDS.md                   ← Already written, copy exactly as provided
│
│   # All 33 role folders are DIRECT children of skills/ — no category dirs.
├── staff-engineer/SKILL.md              ← Build second (orchestrator)
│
│   # Leadership (logical group)
├── pm/SKILL.md
├── growth-pm/SKILL.md
├── em/SKILL.md
├── tech-lead/SKILL.md
├── cto-advisor/SKILL.md
│
│   # Engineering (logical group)
├── swe-fe/SKILL.md
├── swe-be/SKILL.md
├── mobile/SKILL.md
├── ai-ml/SKILL.md
├── api-integration/SKILL.md
├── cryptographic-eng/SKILL.md
├── mlops/SKILL.md
│
│   # Infrastructure (logical group)
├── dpe/SKILL.md
├── release-eng/SKILL.md
├── sre/SKILL.md
├── devops/SKILL.md
├── dba/SKILL.md
├── cloud-architect/SKILL.md
│
│   # Security (logical group)
├── appsec/SKILL.md
├── red-team/SKILL.md
├── secops/SKILL.md
├── compliance/SKILL.md
├── corp-sec/SKILL.md
│
│   # Design (logical group)
├── ux-designer/SKILL.md
├── uxr/SKILL.md
├── content-designer/SKILL.md
├── design-ops/SKILL.md
│
│   # Data (logical group)
├── data-scientist/SKILL.md
├── data-engineer/SKILL.md
├── data-governance/SKILL.md
│
│   # Docs & L10n (logical group)
├── tech-writer/SKILL.md
├── l10n/SKILL.md
│
└── OBSIDIAN-VAULT/
    ├── 00-pipeline-canvas.md
    ├── 01-DOCTRINE.md
    ├── 02-staff-engineer/
    │   └── staff-engineer.md
    ├── 03-leadership/
    │   ├── pm.md
    │   ├── growth-pm.md
    │   ├── em.md
    │   ├── tech-lead.md
    │   └── cto-advisor.md
    ├── 04-engineering/
    │   ├── swe-fe.md
    │   ├── swe-be.md
    │   ├── mobile.md
    │   ├── ai-ml.md
    │   ├── api-integration.md
    │   ├── cryptographic-eng.md
    │   └── mlops.md
    ├── 05-infrastructure/
    │   ├── dpe.md
    │   ├── release-eng.md
    │   ├── sre.md
    │   ├── devops.md
    │   ├── dba.md
    │   └── cloud-architect.md
    ├── 06-security/
    │   ├── appsec.md
    │   ├── red-team.md
    │   ├── secops.md
    │   ├── compliance.md
    │   └── corp-sec.md
    ├── 07-design/
    │   ├── ux-designer.md
    │   ├── uxr.md
    │   ├── content-designer.md
    │   └── design-ops.md
    ├── 08-data/
    │   ├── data-scientist.md
    │   ├── data-engineer.md
    │   └── data-governance.md
    ├── 09-docs-l10n/
    │   ├── tech-writer.md
    │   └── l10n.md
    ├── 10-how-to-use.md
    └── 11-changelog.md
```

---

## SKILL.md Format

Every SKILL.md uses this exact structure. Do not omit any section.

```markdown
---
name: role-identifier
description: >
  One paragraph. What this skill does AND when to trigger it.
  Specific and slightly pushy — Claude undertriggers skills.
  Include role name, domain, stage number, and key trigger phrases.
---

> 📖 Read DOCTRINE.md and ELITE_STANDARDS.md before proceeding. Both are non-negotiable.

## Identity
Who this role is. How they think. What they care about.
What they refuse to tolerate. First person voice. Senior persona, not job description.

## Mental model
The senior judgment layer — specific to this role.
Must include:
- The 3 most common mistakes junior/mid engineers make in this role (things this agent never does)
- The 3 questions this role always asks before starting any task
- The specific failure modes only this role catches — that no other role will catch
- What "legendary" looks like for this specific role
- Current-state-of-field knowledge for 2025 — named technologies, patterns, anti-patterns

## Standards
The concrete output bar for this role specifically.
Must include:
- A checklist of 8–12 items specific to this role (not duplicating ELITE_STANDARDS universals)
- At least 3 named anti-patterns with explanations of why they fail
- At least 3 named patterns with explanations of why they work
- The exact output artifact this role produces and its format
- The exact criteria Staff Engineer uses to pass or fail this role's gate

## Collaboration protocol
- Receives from: [which roles/stages hand off to this role]
- Hands off to: [which roles receive from this role]
- Parallel-safe with: [roles that can run at the same time]
- Escalate to Staff Engineer when: [specific conditions]
- Output format: [exactly what this role produces]

## Workflow
Step-by-step. No gaps. No deferred steps.
Each step fully complete before the next begins.
Executable from the Leadership brief alone — no external input needed.
```

---

## Research Phase — Mandatory Before Every Skill

Before writing any skill file, Claude Code must run a research pass on that role's domain.

**Steps per skill:**
1. Research current best practices for this role in 2025 — production patterns, not tutorials
2. Identify 3–5 companies known for excellence in this domain and what they do differently
3. Research the most common failures in this domain from the last 12 months — real incidents, real lessons
4. Research which tools, libraries, and frameworks are actually in production now vs deprecated
5. Then write the skill file informed by all of the above — not from memory

**Research sources:**
- Engineering blogs: Stripe, Cloudflare, Linear, Vercel, Notion, Figma, GitHub, PlanetScale
- Security: OWASP, CVE database, Google Project Zero
- GitHub trending repositories per domain
- Post-mortems: postmortems.io, major incident analyses
- Conference talks: StrangeLoop, QCon, AWS re:Invent, Google I/O

This research is what separates these skills from generic templates. No skill gets written without it.

---

## Foundation Documents

### DOCTRINE.md
The master law file. Contains exactly:
- The three rules (no skipping, questions only in Stage 1, no stopping)
- Stage gate protocol
- Question window definition (Stage 1 only — explicit and clear)
- Parallel vs sequential execution rules
- Review gate criteria
- Complete list of all 30 skills and their stage assignments

### ELITE_STANDARDS.md
Already written. Copy exactly as provided into skills/ELITE_STANDARDS.md.
Every SKILL.md references it. It defines the elite bar every agent must meet.

### staff-engineer/SKILL.md
The orchestrator. Beyond the standard five sections, must include:

**Routing logic** — how to decompose a task into a Leadership brief, spawn Stage 1 agents via Claude Code's Task tool, what context to pass each agent.

**Stage gate implementation** — exact pass/fail criteria per stage. Not vague — specific.

**Spawn protocol** — what every spawned agent receives: DOCTRINE.md + ELITE_STANDARDS.md + Leadership brief + role-specific instructions + expected output format.

**Correction protocol** — when output fails the gate, specific targeted feedback goes back to the responsible skill. Not "this needs work" — "the auth middleware has no error handling on token expiry, fix before proceeding."

**Parallel coordination** — write conflict resolution when multiple Engineering agents work the same codebase. File-level coordination, handoff format between FE and BE.

---

## Stage-Specific Requirements

### Stage 1 — Leadership
All five agents run in parallel. Combined output is one unified Leadership Brief.

PM runs the intake interview covering minimum:
- What is being built and for whom
- Success criteria and acceptance conditions
- Technical constraints and existing systems
- Non-functional requirements (scale, latency, regions, compliance)
- Anything a downstream stage might need that only the user knows

Growth PM adds: acquisition channels, conversion metrics, onboarding goals, viral mechanics.
Tech Lead adds: preferred stack, architecture constraints, integration points, performance targets.
CTO Advisor adds: build vs buy decisions, long-term architectural implications.
EM adds: delivery sequencing, risk identification, team coordination assumptions.

**Stage 1 output = Leadership Brief so complete that Stages 2–5 never need to ask the user anything.**

### Stage 2 — Engineering
- All output is typed (TypeScript strict, typed Python with mypy)
- All functions have explicit error handling — no bare try/catch, no silent failures
- All APIs have input validation before touching business logic
- All code is observable — structured logging on every meaningful operation
- No hardcoded secrets — env vars with documented names
- Cryptographic Eng must be consulted before any code touching encryption, key management, or auth token design
- SWE-FE and SWE-BE agree on API contracts before either writes implementation
- Mobile consumes the same API contracts as SWE-FE — no separate endpoints
- AI/ML and MLOps coordinate on model serving interface before either builds

### Stage 3 — Infrastructure
- Cloud Architect defines topology first — all other infra skills build within it
- Everything is infrastructure-as-code — no manual console configuration
- All deployments reproducible — same command, same result, every time
- SRE defines SLOs before Release Eng builds the pipeline — pipelines enforce the SLOs
- DBA owns schema migrations — no other skill writes migrations
- Zero-downtime deployments by default — blue/green or canary

### Stage 4 — Security + Design
Security cluster produces a Security Sign-off Document. Design cluster produces a Design Sign-off Document. Neither cluster passes the gate without its sign-off document complete.

Security: AppSec reviews every piece of code. Red Team attempts to break what AppSec approved. SecOps sets alerting based on what Red Team found. Compliance reviews data flows. Corp Security audits IAM.

Design: UX Designer works from the PRD. UXR validates flows against research. Content Designer writes all microcopy and error states. Design Ops ensures all components match the design system.

### Stage 5 — Data & Docs
- Data Engineer builds pipelines before Data Scientist runs analysis
- Data Governance defines access control and lineage for every dataset
- Tech Writer documents every API endpoint, CLI command, and config option — no undocumented surface
- L10n reviews all user-facing copy and flags anything that won't localize

---

## Obsidian Vault Requirements

### 00-pipeline-canvas.md
Full Mermaid diagram of the entire staged pipeline — all 30 skills, all 5 stages, all gates, all parallel relationships. Readable at a glance. Include a legend.

### Per-role notes (folders 02–09)
Each role note contains:
- Role name and one-sentence description
- Stage assignment and parallel group
- What it receives and what it produces
- 3–5 key mental models specific to this role
- Output format
- Links to related roles using Obsidian `[[wikilink]]` syntax — minimum 3 wikilinks per note
- Example trigger phrases

### 10-how-to-use.md
Step-by-step setup guide covering:
1. How to install the skills folder into Claude Code — copy each role folder flat into `~/.claude/skills/` (global) or `<project>/.claude/skills/` (project). Each skill must end up at `.../skills/<role>/SKILL.md`, one level deep. If grouping under a wrapper folder (e.g. `~/.claude/skills/elite-team/<role>/SKILL.md`), confirm the install registers; never nest skills under category folders. Restart Claude Code after copying so new skills register.
2. How to open the Obsidian vault
3. How to trigger the Staff Engineer to start a project
4. What Stage 1 looks like (the question window)
5. How to read the pipeline output
6. How to handle a gate failure
7. Pricing: $39 one-time (mandatory) + $5-7/month optional updates
8. Token note: Claude Pro recommended for full pipeline runs. Claude Max 5x may hit limits on large parallel builds — works fine for individual skill tasks.
9. Update policy: updates ship when the field changes — new standards, new tools, new patterns. Not on a fixed calendar. Not fake version bumps.

### 11-changelog.md
```
## v1.0.0 — Initial release
[List all 30 skills by full name here]
- Staff Engineer orchestrator
- DOCTRINE.md
- ELITE_STANDARDS.md
- Full Obsidian vault
```

---

## Build Order

Execute in this exact order. Complete each file fully before moving to the next.
All role folders are flat — direct children of `skills/`. No category directories.

```
1.  skills/DOCTRINE.md
2.  skills/ELITE_STANDARDS.md          ← copy from provided file exactly
3.  skills/staff-engineer/SKILL.md
4.  skills/pm/SKILL.md
5.  skills/growth-pm/SKILL.md
6.  skills/em/SKILL.md
7.  skills/tech-lead/SKILL.md
8.  skills/cto-advisor/SKILL.md
9.  skills/swe-fe/SKILL.md
10. skills/swe-be/SKILL.md
11. skills/mobile/SKILL.md
12. skills/ai-ml/SKILL.md
13. skills/api-integration/SKILL.md
14. skills/cryptographic-eng/SKILL.md
15. skills/mlops/SKILL.md
16. skills/dpe/SKILL.md
17. skills/release-eng/SKILL.md
18. skills/sre/SKILL.md
19. skills/devops/SKILL.md
20. skills/dba/SKILL.md
21. skills/cloud-architect/SKILL.md
22. skills/appsec/SKILL.md
23. skills/red-team/SKILL.md
24. skills/secops/SKILL.md
25. skills/compliance/SKILL.md
26. skills/corp-sec/SKILL.md
27. skills/ux-designer/SKILL.md
28. skills/uxr/SKILL.md
29. skills/content-designer/SKILL.md
30. skills/design-ops/SKILL.md
31. skills/data-scientist/SKILL.md
32. skills/data-engineer/SKILL.md
33. skills/data-governance/SKILL.md
34. skills/tech-writer/SKILL.md
35. skills/l10n/SKILL.md
36. skills/OBSIDIAN-VAULT/00-pipeline-canvas.md
37. skills/OBSIDIAN-VAULT/01-DOCTRINE.md
38. skills/OBSIDIAN-VAULT/02-staff-engineer/staff-engineer.md
39. skills/OBSIDIAN-VAULT/03-leadership/ (all 5 notes)
40. skills/OBSIDIAN-VAULT/04-engineering/ (all 7 notes)
41. skills/OBSIDIAN-VAULT/05-infrastructure/ (all 6 notes)
42. skills/OBSIDIAN-VAULT/06-security/ (all 5 notes)
43. skills/OBSIDIAN-VAULT/07-design/ (all 4 notes)
44. skills/OBSIDIAN-VAULT/08-data/ (all 3 notes)
45. skills/OBSIDIAN-VAULT/09-docs-l10n/ (all 2 notes)
46. skills/OBSIDIAN-VAULT/10-how-to-use.md
47. skills/OBSIDIAN-VAULT/11-changelog.md
```

---

## Quality Bar

Every SKILL.md must pass this checklist before it is done:

- [ ] YAML frontmatter complete (name, description with trigger phrases)
- [ ] Opens with reference to both DOCTRINE.md and ELITE_STANDARDS.md
- [ ] All five sections present and fully written
- [ ] Identity: first-person senior voice, not a job description
- [ ] Mental model: role-specific, opinionated, includes 3 mistakes/3 questions/failure modes/what legendary looks like/2025 field knowledge
- [ ] Standards: role-specific checklist 8–12 items, 3 anti-patterns, 3 patterns, output artifact format, gate criteria
- [ ] Collaboration protocol: exact inputs, outputs, parallel-safe roles, escalation conditions
- [ ] Workflow: step-by-step, no gaps, no deferred steps
- [ ] Under 500 lines — if approaching limit, split into SKILL.md + references/ subfolder
- [ ] No TODOs anywhere
- [ ] Research phase completed before writing — skill reflects 2025 current-state knowledge
- [ ] Obsidian note uses wikilinks to minimum 3 related roles

---

## Completion Criteria

The build is complete when ALL of the following are true:

1. All 35 skill files exist and pass the quality bar
2. DOCTRINE.md and ELITE_STANDARDS.md exist in skills/ root
3. Both are referenced in every SKILL.md
4. All Obsidian vault files exist with correct wikilinks
5. The pipeline canvas Mermaid diagram renders correctly
6. The how-to-use guide covers all 9 topics listed above including pricing and token note
7. The changelog v1.0.0 lists all 30 skills by full name
8. Every skill reflects 2025 current-state-of-field knowledge from the research phase
9. Staff Engineer skill includes routing, gate, spawn, correction, and coordination protocols
10. Every role folder is flat — `skills/<role>/SKILL.md`, one level deep, no category directories. Verify with `find skills -name SKILL.md | wc -l` (expect 33) and confirm no path contains a category folder segment (e.g. `engineering/`, `security/`).

Do not stop before all 10 criteria are met.

---

*Brief version: 2.0 — Final approved. Ready for Claude Code execution.*
