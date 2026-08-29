---
cssclasses:
  - elite-doc
---

# How to Use

> Setup and operating guide for the AI Engineering Org skill team. Read [[DOCTRINE]] for the law and
> open [[pipeline]] for the map. This guide takes you from install to a delivered pipeline.

---

## 1. Install the skills folder into Claude Code

Claude Code discovers skills from a `skills/` directory placed where it looks for them. You have two
choices:

- **User-level (available in every project):** copy the entire `skills/` folder to
  `~/.claude/skills/`.
  ```bash
  cp -R skills ~/.claude/skills
  ```
- **Project-level (scoped to one repo):** copy it into the project's `.claude/skills/`.
  ```bash
  mkdir -p .claude && cp -R skills .claude/skills
  ```

Claude Code finds each skill by reading the `SKILL.md` files: it scans for `SKILL.md`, parses the YAML
frontmatter (`name` + `description`), and uses the `description` to decide when to trigger that skill.
Keep the folder structure intact — `DOCTRINE.md`, `ELITE_STANDARDS.md`, the `staff-engineer/SKILL.md`,
and the role folders must all be present, because every skill references DOCTRINE.md and
ELITE_STANDARDS.md and the Staff Engineer spawns the rest. Verify the install:
```bash
find ~/.claude/skills -name SKILL.md | wc -l   # expect 34 (33 specialists + staff-engineer)
```

---

## 2. Open the Obsidian vault

The `OBSIDIAN-VAULT/` folder **is** the vault. In Obsidian: **Open folder as vault** → select
`skills/OBSIDIAN-VAULT/`. The numbered notes (`00`–`11`) and the role folders (`02`–`09`) load with all
`[[wikilinks]]` live. Open [[pipeline]] first (it renders the Mermaid diagram of the whole
pipeline), then use the graph view to navigate between roles. Every role note links to at least three
related roles, so the graph mirrors the real handoffs.

---

## 3. Trigger the Staff Engineer to start a project

The [[staff-engineer|Staff Engineer]] is the entry point for anything non-trivial. In
a Claude Code session, describe what you want built in one message — e.g. *"Build and ship a multi-tenant
billing service with a dashboard,"* or *"Take this idea from concept to production."* Phrases like
**build, ship, design and implement, stand up a service, run the pipeline** trigger the orchestrator. It
will own the task end to end: it is the only skill that spawns the others, so you talk to it, not to
each specialist. For a tiny single-role task you can name a specialist directly (e.g. "AppSec review
this file"), but anything spanning more than one role should go through the Staff Engineer.

---

## Two operating modes — Build & Upgrade

The org runs in one of two modes; the Staff Engineer picks one (or you tell it).

- **Build Mode** *(greenfield)* — a new project runs through **all five stages** in order, gate by gate, building a production-grade system from the Leadership Brief.
- **Upgrade Mode** *(brownfield)* — applied to an **existing codebase**: the Staff Engineer assesses the current state, then runs **only the stages a change actually touches**, still enforcing every gate and still requiring the [[qa-engineer|QA Engineer]]'s independent audit before sign-off. Use it to harden, extend, or modernize without a full rebuild.

To choose, say "build mode" / "upgrade mode" when you trigger the Staff Engineer, or just describe the situation (new project vs. existing system) and it will infer.

## 4. What Stage 1 looks like (the question window)

Stage 1 (Leadership) is the **only** stage that asks you questions. The Staff Engineer spawns
[[pm|PM]] (who runs a structured intake interview) alongside
[[growth-pm|Growth PM]], [[em|EM]], [[tech-lead|Tech Lead]],
and [[cto-advisor|CTO Advisor]]. Expect questions covering: what's being built and for
whom, success criteria and acceptance conditions, technical constraints and existing systems,
non-functional requirements (scale, latency, regions, compliance), acquisition/onboarding goals, stack
and integration preferences, and build-vs-buy. Answer thoroughly here — this is your one window. The
output is a single **Leadership Brief** complete enough that Stages 2–5 never need to ask you anything.
If you're unsure about something, say so; the brief records assumptions explicitly.

---

## 5. How to read the pipeline output

After Stage 1, the pipeline runs Stages 2→5 in sequence (see [[pipeline]]). You'll receive:
- The **Leadership Brief** (the agreed spec).
- A **per-stage ownership + ordering plan** (which agent owns which files).
- A **gate record per stage** — pass/fail with the evidence for each of the three gate questions.
- The **Security Sign-off Document** and the **Design Sign-off Document** from Stage 4.
- The **final delivery summary** mapping every requirement to the artifact that satisfies it.
Read the gate records to see how each stage was held to the bar, and the final summary to confirm every
completion criterion is met. Production code, infrastructure, sign-off docs, and documentation are the
deliverables — not a prototype.

---

## 6. How to handle a gate failure

A gate failure is normal and healthy — it means the Staff Engineer caught something before it shipped.
When a gate fails, it returns a **targeted correction** to the responsible role in the form
**file → defect → required fix** (never a vague "needs work"), then re-runs only the corrected artifact
plus anything that consumed it. You don't have to do anything: the loop is internal. If a failure is
caused by a genuine blocker that only you can resolve (a credential, a private hostname, a legal entity
name), the Staff Engineer surfaces it with options and a recommendation — answer it and the pipeline
continues. Everything else converges automatically.

---

## 7. Pricing

- **$39 one-time** — mandatory. This buys the complete org: 33 specialist skills + the Staff Engineer
  orchestrator, DOCTRINE.md, ELITE_STANDARDS.md, and the full Obsidian vault. Yours to use, forever, at
  the version you bought.
- **$5–7 / month — optional.** A subscription that ships updates as the field changes (see Topic 9). The
  product is fully functional without it; the subscription keeps it current.

---

## 8. Token note (which Claude plan to run on)

Running the full pipeline spawns many specialist agents in parallel, which consumes tokens.
- **Claude Pro** is recommended for full end-to-end pipeline runs.
- **Claude Max 5x** can hit usage limits on large parallel builds (Stage 2 and Stage 4 fan out widely).
  It works fine for individual skill tasks (e.g. a single AppSec review or a UX flow) and smaller
  pipelines, but very large parallel builds may pause on limits. For the biggest builds, prefer Pro or
  run stages in sequence rather than maximizing parallel fan-out.

---

## 9. Update policy

Updates ship **when the field changes** — a new standard, a new tool, a new pattern, a notable incident
worth encoding — **not on a fixed calendar and never as fake version bumps**. When OWASP revises its Top
10, when a new experimentation or localization standard lands, when a supply-chain incident teaches a
new lesson, the affected skills are updated and the change is recorded in [[changelog]]. You will not
see manufactured "v2 / v3" releases padded with nothing; a version exists only when there is real new
state-of-field knowledge to deliver.

---

> Next steps: skim [[DOCTRINE]] so you know the rules the system holds itself to, open
> [[pipeline]] to see the flow, and trigger the
> [[staff-engineer|Staff Engineer]] with your first task.
