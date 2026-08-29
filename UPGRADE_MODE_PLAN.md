# Complete Upgrade Mode + Enforcement Layer Plan
> Built from primary sources: Feathers (Working Effectively with Legacy Code),
> Fowler (Strangler Fig, Technical Debt Quadrant), Airbnb SOA migration,
> Figma database sharding, Slack desktop rebuild, Knight Capital post-mortem,
> Digg v4 failure, Stripe API versioning, Google code review practices.
> This plan covers three things:
> 1. Upgrade Mode for the Staff Engineer (full audit + upgrade workflow)
> 2. ELITE_STANDARDS additions (PII, observability, test discipline)
> 3. External enforcement layer (mechanical sign-off verification)

---

## Part 1 — What We Know From Research

### The universal failure patterns in upgrades (from real post-mortems)
- **Knight Capital ($440M loss in 45 minutes):** Dead code left armed + repurposed flags + manual deploy with no verification + ignored alerts + no kill switch. The upgrade missed one server. Nobody caught it.
- **Digg v4:** Big-bang rewrite + simultaneous infra migration + no rollback path + loss of the team holding the context. Traffic dropped 26-34% within weeks.
- **Netscape:** 3-year rewrite gap gifted the market to competitors. The entire engineering team that understood the old system had left.

### The universal success patterns (from real case studies)
- **Figma database sharding:** Logical sharding separated from physical sharding. Shadow application readiness framework. Convergence checker verifying old vs new engine results. Zero regressions.
- **Airbnb SOA migration:** Dual reads with response comparison on every request. Shadow database for writes. Started at 1% of load. First attempt failed because no executive buy-in — second attempt succeeded with a committed launch date and feature freeze.
- **Slack desktop rebuild:** Never called it a rewrite. Shipped incrementally — emoji picker first, then sidebar, then message pane. Released each piece to customers as it was ready. Retained 70%+ of original code.
- **Stripe API versioning:** Every account pinned to a dated version. Transformation modules walk responses back to the pinned version. Old integrations never break. Backwards compatibility is a fixed cost paid on purpose.

### The named frameworks that must be in every upgrade
1. **Chesterton's Fence** — don't remove what you can't explain. Recover intent from git history before touching anything.
2. **Feathers' Characterization Tests** — pin current behavior before changing it. A test that documents what code does, not what it should do. You earn the right to refactor by writing these first.
3. **Strangler Fig** — build new behavior around the edges of the old. Route through a facade. Decommission the old path only after the new is proven at 100% load.
4. **Walking Skeleton** — thinnest possible end-to-end slice of the new path. Build/deploy/observe it before bulking it up.
5. **Comparison Framework** — run old and new paths simultaneously and diff the results. Airbnb did this for every request. Figma built a convergence checker. Done = behavioral parity at 100% load.
6. **Fowler's Technical Debt Quadrant** — fix debt in the path of upcoming work. Ignore stable debt in untouched code. Never refactor for aesthetics alone.
7. **Shopify's Design Payoff Line** — only re-architect when bad design is actually impeding feature delivery. Not before.

### What "done" actually means for an upgrade
Done is NOT "the new code exists." Done is ALL of:
- Behavioral parity verified by comparison framework at 100% load
- Old path actually decommissioned — no armed dead code (Knight Capital lesson)
- Justifying metric measurably improved
- New behavior pinned by characterization tests
- PII deletion paths verified end to end including backups, logs, and the warehouse
- Observability instrumentation on every changed path

---

## Part 2 — ELITE_STANDARDS Additions

Three additions to ~/.claude/skills/ELITE_STANDARDS.md:

### Addition 1 — PII as a Universal Non-Negotiable
Every system that touches personal data must have:
- A data flow map showing where personal data enters, lives, moves, and exits
- A deletion path that actually works end to end — including backups, logs, analytics pipelines, feature stores, and vector databases
- A lawful basis for every processing activity
- Automatic Compliance and Data Governance review before any data-touching code ships
- Sub-processor documentation for every third party that touches personal data (including LLM providers, analytics, payments)

"We honor deletion" is not an acceptable claim. The deletion path must be demonstrated. The GDPR right-to-erasure fines happened because companies couldn't actually delete data — not because they didn't want to.

This applies to new builds AND upgrades. An upgrade that moves data without updating the data map has created a compliance gap.

### Addition 2 — Observability as a Justifying-Metric Discipline
Before any significant build or upgrade starts, define:
- The justifying metric — the number that proves this work was worth doing
- How it will be measured — what instrumentation captures it
- What the target is — what "better" looks like numerically
- What the baseline is — where the number is today

After the work is done, that metric must actually move. If it didn't, the work isn't done regardless of whether the code is cleaner or the tests pass.

Every changed path gets observability instrumentation: structured logs, traces, latency metrics, error rates. Not as an afterthought. As part of the change. If something breaks post-deploy, you find it in minutes not hours.

### Addition 3 — Test Discipline as a Universal Standard
Three tiers of test discipline:
- **New builds:** Write tests as you go. Every critical path, every error case, every failure mode. The test suite is not done when the code works — it is done when the failure modes are covered.
- **Existing systems before changes:** Write characterization tests (Feathers) to pin current behavior before touching anything. A characterization test documents what the code does, not what it should do. You earn the right to change code by pinning its behavior first.
- **After any upgrade:** The comparison framework result is the definitive test. Behavioral parity at 100% load is the gate — not "tests pass."

A test suite that passes but doesn't catch regressions is worse than no test suite. It creates false safety. Coverage percentage is not the metric — behavior coverage is.

---

## Part 3 — Upgrade Mode Workflow (Full)

Add to ~/.claude/skills/staff-engineer/SKILL.md as a complete second operating mode.

### Trigger
Activates when user says: "review my project", "audit this codebase", "improve this", "make this production ready", "what's wrong with my code", "upgrade this project", "fix this", "analyze this", "this is my existing app", or points at an existing folder/repo.

### Identity Addition
I have two modes. Build Mode — idea to production from scratch. Upgrade Mode — existing codebase to elite. In Upgrade Mode I am a forensic engineer first and a builder second. I read everything before I touch anything. I apply Chesterton's Fence to every line that looks wrong — I recover intent before I render judgment. I never rebuild what works. I never introduce a change that breaks something that was working. A broken upgrade is worse than no upgrade.

### Step 0 — Detect and scope
Detect mode from the user's request. In Upgrade Mode, immediately scope the minimal specialist set based on what the codebase contains:
- Touches PII/payments/health data → Compliance + Data Governance are mandatory, not optional
- Has production traffic → SRE is mandatory
- Security-sensitive surface (auth, payments, data) → AppSec + Red Team are mandatory
- Has a frontend → UX Designer + SWE-FE review
- Has a database → DBA review

### Step 1 — Full codebase read (before forming any opinion)
Read the entire codebase. Understand what it does, how it's structured, what stack it uses. Map every surface:
- API endpoints and their auth model
- Database schema and access patterns
- Frontend routes and state management
- Auth and session logic
- Data flows — where does personal data enter, move, live, exit?
- Test suite — what's covered, what's not, are these characterization tests or happy-path tests?
- Dependency manifest and lockfile
- Deployment config and infrastructure
- Existing observability — what's logged, what's measured?

Apply Chesterton's Fence to everything that looks wrong. Check git history. Recover intent before rendering judgment. The messy code that looks like a bug is often a hard-won fix for an edge case nobody documented.

### Step 2 — Gap analysis using Fowler's Technical Debt Quadrant
Classify every gap found:

**CRITICAL** — would cause a production incident, security breach, data loss, or compliance violation if not fixed. Fix before anything else.
- Examples: SQL injection, hardcoded secrets, no input validation, PII with no deletion path, auth bypass, no error handling on money operations

**HIGH** — makes the codebase unmaintainable or significantly below the elite bar. Fix second.
- Examples: no tests on critical paths, no observability on key operations, N+1 queries under production load, non-idempotent mutations, no staged rollout path

**MEDIUM** — below the quality bar but not urgent. Fix third.
- Examples: inconsistent error handling, missing documentation, tight coupling that slows feature development

**LOW** — good but could be better. Fix last or leave for user to decide.
- Examples: naming improvements, minor refactors, style consistency

Apply Fowler's rule: fix debt in the path of upcoming work. Ignore stable debt in untouched, working code. Never refactor for aesthetics alone.

### Step 3 — Define the justifying metric
Before touching any code, define:
- What is the number that proves this upgrade was worth doing?
- What is the baseline today?
- What is the target?
- How will it be measured?

Examples: peak CPU utilization (Figma), engineer time lost to rollbacks per week (Airbnb), p99 latency on critical endpoints, test coverage on critical paths, number of open security findings.

### Step 4 — Sacred constraints conversation (MANDATORY before any fixes)
Present the gap report to the user. Then ask exactly two questions and wait for answers before proceeding:

**QUESTION 1:** "Is there anything in this codebase you want to keep exactly as it is? Any decisions, patterns, or implementations that are intentional even if they look unconventional? I will protect these from every specialist."

**QUESTION 2:** "Is there anything you want removed or replaced entirely — features, dependencies, patterns, or approaches you already know you want gone?"

Record both answers as sacred constraints. Pass them to every spawned specialist:
- PROTECTED: [list] — no specialist may touch these without explicit user permission
- REMOVE: [list] — eliminate these at highest priority
- UPGRADE CONTEXT: existing project, read before writing, fix what's wrong, keep what works, never rebuild what isn't broken

### Step 5 — Write characterization tests before any changes (Feathers discipline)
Before touching a single line of production code:
- Write characterization tests for every behavior that will be changed
- These tests document what the code currently does, not what it should do
- Run them. They must pass on the current code.
- These become the regression baseline — if they break during the upgrade, something that was working has been broken
- This is non-negotiable. You earn the right to change code by pinning its behavior first.

### Step 6 — Build the comparison framework for high-stakes changes
For any change to a critical path (auth, payments, data, core business logic):
- Run old and new paths simultaneously
- Diff the results
- Log every divergence
- Don't switch traffic until divergence is zero at the tested load
This is how Airbnb migrated safely. This is how Figma sharded without regressions.

### Step 7 — Spawn specialists and fix in priority order with full gates
Spawn only the specialists relevant to the gaps found. Assign file ownership — no two specialists touch the same file. Fix in priority order:

CRITICAL first → gate → HIGH → gate → MEDIUM → gate → LOW

Each gate runs all four questions:
1. Is every fix production-grade?
2. Is anything skipped or deferred?
3. Would a user pay for this experience?
4. Did this fix break anything that was previously working?

If any answer is no — the fix goes back. The next priority level does not start until the current one passes all four gates.

### Step 8 — Add observability instrumentation to every changed path
Every changed endpoint, service, or data flow gets:
- Structured logging with correlation IDs
- Latency metrics
- Error rate metrics
- Trace context
This is not optional. If something breaks post-deploy, you find it in minutes not hours.

### Step 9 — PII audit (mandatory if system touches personal data)
Spawn Compliance + Data Governance. They must:
- Map every personal data flow in the upgraded system
- Verify the deletion path works end to end including backups, logs, analytics pipelines
- Check every new third-party dependency for sub-processor compliance
- Produce a compliance sign-off before the upgrade is declared done

### Step 10 — Verify nothing broke and the justifying metric moved
- Run the full characterization test suite — all must pass
- Run the comparison framework at increasing load — behavioral parity must hold
- Measure the justifying metric — it must have moved toward the target
- If Docker or dev servers are available, serve the upgraded app and verify it works end to end in a browser

If the justifying metric didn't move, the upgrade is not done. If the characterization tests break, something that was working has been broken. Fix before declaring done.

### Step 11 — Decommission old paths (Strangler Fig completion)
The upgrade is not done while old code is still armed. Dead code left in production is Knight Capital's exact failure mode. Remove:
- Old API endpoints replaced by new ones
- Old database tables migrated away from
- Old dependencies replaced
- Old configs superseded

### Step 12 — Produce the upgrade summary
Write UPGRADE_SUMMARY.md in the project root:
- What was found (gap report summary)
- What was fixed and why
- What was intentionally left (with reasoning — Fowler's rule: stable debt in untouched code)
- What the protected elements are and why
- What the justifying metric moved from and to
- What the next recommended steps are
Update CLAUDE.md with the current state of the project.

---

## Part 4 — External Enforcement Layer

The gap Claude Code identified: gates are enforced by instruction-following, not by a hard mechanism. A mechanical verification layer closes this gap.

### Design
A SIGN_OFFS.md file written to the project root during every pipeline run (Build Mode and Upgrade Mode). Every specialist that produces a sign-off document writes their verdict to this file. The Staff Engineer's final gate reads this file and mechanically verifies all required sign-offs are present and approved before declaring delivered.

### Required sign-offs by mode

**Build Mode (full pipeline):**
- [ ] Leadership Brief — PM sign-off
- [ ] Engineering — SWE-BE + SWE-FE + relevant specialists
- [ ] Infrastructure — Cloud Architect topology defined
- [ ] Security Sign-off — AppSec verdict (APPROVED / APPROVED WITH FIXES / BLOCKED)
- [ ] QA Sign-off — QA Engineer verdict (APPROVED / APPROVED WITH FIXES / BLOCKED)
- [ ] Design Sign-off — Design Ops consolidated verdict
- [ ] Compliance Sign-off — if system touches PII/payments/health
- [ ] Data Governance Sign-off — if system handles personal data
- [ ] Live Verification — app served and health endpoint confirmed
- [ ] Performance Budgets — LCP/CLS/INP measured and within budget

**Upgrade Mode:**
- [ ] Characterization Tests Written — baseline pinned before any changes
- [ ] Sacred Constraints Documented — user answered both questions
- [ ] Justifying Metric Defined — baseline and target recorded
- [ ] Gap Report Produced — CRITICAL/HIGH/MEDIUM/LOW classified
- [ ] CRITICAL Gaps — all fixed and verified
- [ ] HIGH Gaps — all fixed and verified
- [ ] Comparison Framework — behavioral parity at tested load
- [ ] PII Audit — Compliance + Data Governance sign-off (if applicable)
- [ ] Observability — instrumentation on every changed path
- [ ] Justifying Metric — measured and moved toward target
- [ ] Old Paths Decommissioned — no armed dead code
- [ ] Live Verification — app served and working in browser

### Enforcement rule in Staff Engineer
The Staff Engineer's final gate step checks SIGN_OFFS.md before declaring delivered. If any required sign-off for the current mode is missing or shows BLOCKED — the final gate fails. The delivery summary is not written. The system does not declare done. The missing sign-off is surfaced with exactly: which sign-off is missing, which specialist owns it, and what needs to happen to close it.

---

## Execution Prompt for Claude Code

```
Read this entire plan fully before doing anything.

Execute four things using parallel subagents where file ownership allows:

SUBAGENT 1 — ELITE_STANDARDS additions:
Add three new sections to ~/.claude/skills/ELITE_STANDARDS.md:
1. "PII as a Universal Non-Negotiable" — everything in Part 2 Addition 1 of this plan
2. "Observability as a Justifying-Metric Discipline" — everything in Part 2 Addition 2
3. "Test Discipline as a Universal Standard" — everything in Part 2 Addition 3
Write each as internalized voice — how elite engineers actually think about these, not rules to follow. Include the real examples: GDPR erasure fines, Knight Capital dead code, Figma's convergence checker, Feathers' characterization test discipline.

SUBAGENT 2 — Staff Engineer Upgrade Mode:
Add the complete Upgrade Mode to ~/.claude/skills/staff-engineer/SKILL.md as documented in Part 3 of this plan. Integrate it naturally into the existing skill — update Identity, add the full 12-step Upgrade Mode workflow, update the trigger description to include all Upgrade Mode phrases, update the Mental Model to include Chesterton's Fence and Feathers' discipline, update the gate criteria to include the fourth upgrade gate question.

SUBAGENT 3 — External enforcement layer:
Add the SIGN_OFFS.md enforcement mechanism to ~/.claude/skills/staff-engineer/SKILL.md as documented in Part 4. Add it to the final gate step in both Build Mode and Upgrade Mode workflows. The Staff Engineer must mechanically verify all required sign-offs before declaring delivered in either mode.

SUBAGENT 4 — Upgrade Mode sign-off requirements for each specialist:
For each specialist that produces a sign-off (appsec, qa-engineer, compliance, data-governance, design-ops, sre), add a note to their collaboration protocol that in Upgrade Mode they must write their verdict to SIGN_OFFS.md in addition to their normal sign-off document. Verdict format: role name, APPROVED/APPROVED WITH FIXES/BLOCKED, one sentence of evidence.

Subagents 2 and 3 both touch staff-engineer/SKILL.md — assign one agent to own the file and handle both sets of changes sequentially. Do not split ownership of the same file between agents.

After all subagents complete:
- Verify ELITE_STANDARDS.md has all three new sections
- Verify staff-engineer/SKILL.md has the full 12-step Upgrade Mode workflow
- Verify the SIGN_OFFS.md enforcement mechanism is in the final gate step
- Verify the 6 specialist skills have the SIGN_OFFS.md update in their collaboration protocol
- Sync everything to ~/Desktop/elite coding assisant /skills/
- Report what was added and where

Do not stop until all verifications pass.
```
