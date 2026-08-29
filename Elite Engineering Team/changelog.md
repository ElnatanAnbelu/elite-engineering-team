---
cssclasses:
  - elite-doc
---

# Changelog

> Updates ship when the field changes — new standards, tools, or patterns — not on a fixed calendar and
> never as fake version bumps (see [[how-to-use]], Topic 9). Each entry records real new
> state-of-field knowledge delivered into the skills.

---

## v1.1.0 — Pipeline restructure & the QA gate

Structural changes to the org and a new operating model.

### Structure changes
- **Design roles became the Discovery cluster in Stage 1 (Leadership + Discovery).** [[ux-designer|UX Designer]], [[uxr|UXR]], [[content-designer|Content Designer]], and [[design-ops|Design Ops]] now run *inside* the Leadership stage — design starts with the brief, not after engineering. **Stage 1 is now 9 roles.**
- **[[mlops|MLOps]] moved from Stage 2 (Engineering) to Stage 3 (Infrastructure).** Serving, monitoring, and the eval-gated retraining pipeline live with the infra layer; MLOps still agrees the serving interface with [[ai-ml]] (Stage 2) first. **Stage 3 is now 7 roles.**
- **New role — [[qa-engineer|QA Engineer]] added to Stage 4.** An independent quality gate: verifies a real test pyramid, end-to-end critical paths, performance budgets, accessibility, and zero flake before security sign-off. **Stage 4 is now Security + QA (6 roles)**; the old Design cluster is gone from this stage.
- **Total specialists: 33** (was 30) + the Staff Engineer orchestrator.

### New operating modes
- **Build Mode** *(greenfield)* — a task runs through all five stages start-to-finish to build a new system.
- **Upgrade Mode** *(brownfield)* — the pipeline is applied to an existing codebase: assess current state, then run only the stages a change touches, with the QA Engineer's independent audit and every gate still enforced.

### Vault updates
- Pipeline canvas redrawn (Stage 1 = 9 roles; Stage 4 = 6 incl. QA Engineer).
- Org Map spine canvas regenerated for the new stage structure.
- Role-note stage assignments corrected (Design → Stage 1, MLOps → Stage 3); Security notes rewired to QA.
- DOCTRINE roster, HOME dashboard, how-to-use, and graph colours updated to 33 specialists.

---

## v1.0.0 — Initial release

The complete AI Engineering Org: **30 specialist skills + the Staff Engineer orchestrator**, the two
foundation documents, and the full Obsidian knowledge vault.

### Orchestrator
- **Staff Engineer (staff-engineer)** — routing, stage gates, spawn protocol, correction protocol, and
  parallel coordination across the five-stage pipeline.

### Stage 1 — Leadership
1. **Product Manager (pm)**
2. **Growth PM (growth-pm)**
3. **Engineering Manager (em)**
4. **Tech Lead (tech-lead)**
5. **CTO Advisor (cto-advisor)**

### Stage 2 — Engineering
6. **Software Engineer, Frontend (swe-fe)**
7. **Software Engineer, Backend (swe-be)**
8. **Mobile Engineer (mobile)**
9. **AI/ML Engineer (ai-ml)**
10. **API Integration Engineer (api-integration)**
11. **Cryptographic Engineer (cryptographic-eng)**
12. **MLOps Engineer (mlops)**

### Stage 3 — Infrastructure
13. **Developer Productivity Engineer (dpe)**
14. **Release Engineer (release-eng)**
15. **Site Reliability Engineer (sre)**
16. **DevOps Engineer (devops)**
17. **Database Administrator (dba)**
18. **Cloud Architect (cloud-architect)**

### Stage 4 — Security
19. **Application Security Engineer (appsec)**
20. **Red Team Engineer (red-team)**
21. **Security Operations Engineer (secops)**
22. **Compliance Specialist (compliance)**
23. **Corporate Security Engineer (corp-sec)**

### Stage 4 — Design
24. **UX Designer (ux-designer)**
25. **UX Researcher (uxr)**
26. **Content Designer (content-designer)**
27. **Design Ops (design-ops)**

### Stage 5 — Data & Docs
28. **Data Scientist (data-scientist)**
29. **Data Engineer (data-engineer)**
30. **Data Governance Specialist (data-governance)**
31. **Technical Writer (tech-writer)**
32. **Localization Specialist (l10n)**

> The list above shows all skills by full name in pipeline position. The product is **30 specialist
> skills + the Staff Engineer orchestrator** — the line numbers reflect pipeline order, not extra
> specialists beyond the 30.

### Foundation documents
- **DOCTRINE.md** — the master law: the three rules, stage-gate protocol, question window, and
  parallel-vs-sequential execution rules.
- **ELITE_STANDARDS.md** — the shared bar for "done": the five pillars and the universal non-negotiables
  every skill is held to.

### Obsidian vault
- The full **Obsidian knowledge vault**: the pipeline canvas ([[pipeline]]), the DOCTRINE
  companion ([[DOCTRINE]]), the Staff Engineer note
  ([[staff-engineer|staff-engineer]]), a role note for all 30 specialists across
  the stage folders, the setup guide ([[how-to-use]]), and this changelog — fully cross-linked with
  `[[wikilinks]]` and a rendered pipeline diagram.

---

*Future entries will appear above this line as the field moves and the skills are updated.*
