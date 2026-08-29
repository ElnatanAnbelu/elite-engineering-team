# Issues & Fixes Plan — Elite Engineering Skill Team
> Living document. Updated after every test. Fix in order of priority.

---

## Status Legend
- 🔴 Open — not fixed
- 🟡 Partial — mechanism in place, not fully verified
- ✅ Closed — fixed and verified

---

## Issue 1 — Task tool / parallel subagents not firing
**Status:** 🔴 Open
**What happened:** Staff Engineer tried to spawn parallel subagents via the Task tool and got "invalid tool parameters." It correctly fell back to sequential execution with the same doctrine and gates — output quality was identical — but parallel execution is the designed behavior.
**Impact:** Performance only. Quality is not affected. Sequential execution under DOCTRINE produces the same output, just slower.
**Fix needed:** Investigate whether Claude Code terminal supports the Task tool with specific flags (e.g. `--dangerously-skip-permissions`). If not available in standard terminal, document sequential as the supported mode and update the pipeline canvas accordingly.
**Priority:** Medium — doesn't affect output quality, affects speed.

---

## Issue 2 & 3 — 513 competing skills / had to explicitly call staff-engineer
**Status:** ✅ Closed
**What happened:** `~/.claude/skills/` had 513 SKILL.md files from previous installs. Claude Code grabbed Superpowers skill on first attempt. User had to explicitly say "use staff-engineer."
**Fix applied:** Backed up 49 non-elite skills to `~/claude-skills-backup/`. Only 35 items remain in `~/.claude/skills/` (33 skills + DOCTRINE.md + ELITE_STANDARDS.md).
**Verified:** Second full-stack test triggered staff-engineer automatically without explicit calling.
**Remaining caveat:** Plugin skills (gstack, superpowers, claude-mem) live in plugin caches, not `~/.claude/skills/`. They didn't interfere in the second test but still exist.

---

## Issue 4 — No session context persistence between terminals
**Status:** ✅ Closed
**What happened:** Closing terminal lost all project context. New session re-discovered everything from scratch.
**Fix applied:** Added CLAUDE.md session summary step to Staff Engineer's Step 7. Every pipeline run now produces a CLAUDE.md in the project root with full context.
**Verified:** Second test produced CLAUDE.md in `~/test-marketplace/`.

---

## Issue 5 — Pipeline doesn't run the app end-to-end in a browser
**Status:** 🔴 Open
**What happened:** The pipeline built and tested everything correctly (unit tests, smoke tests, typecheck, zero vulnerabilities) but couldn't serve the app in a browser for final human verification. Port 8080 didn't open because Docker daemon wasn't running during the pipeline run.
**Impact:** High for user confidence. Users expect to see something running in a browser, not just passing tests.
**Fix needed:** Add a final verification step to the Staff Engineer's Step 7 that:
1. Detects whether Docker is available and running
2. If yes — runs `docker compose up --build` and confirms the app loads on the expected port
3. If no — runs the app directly (backend + frontend dev servers) and confirms health endpoints respond
4. Reports the live URL to the user as part of the delivery summary
**Priority:** High — this is what users see at the end of the pipeline.

---

## Issue 6 — Plugin cache competition still exists
**Status:** 🔴 Open
**What happened:** Plugin skills (gstack, superpowers, claude-mem, marketing-skills) live in plugin caches separate from `~/.claude/skills/`. They didn't interfere in the second test but could in future sessions depending on trigger matching.
**Impact:** Low right now. Could cause wrong skill activation in edge cases.
**Fix needed:** Investigate whether plugin skills can be disabled or scoped. If not, strengthen the staff-engineer trigger description to be more dominant over plugin triggers.
**Priority:** Low — not currently causing problems.

---

## Issue 7 — Leadership Stage doesn't extract enough product-specific context
**Status:** 🔴 Open
**What happened:** In both tests the PM asked structured technical questions but the intake was somewhat generic. It covered technical requirements well but didn't deeply understand the product vision — what kind of app the user actually wants to build, who the real users are, what problem it solves, what makes it different from existing solutions.
**Impact:** Critical — highest priority. If Leadership doesn't fully understand what you want, every downstream stage builds the wrong thing correctly. A technically perfect app that solves the wrong problem is a total failure.
**Fix needed:** Strengthen the PM skill's intake interview to extract product vision, not just technical requirements. Must add:
- The core user problem being solved (in the user's words)
- Who specifically are the users — buyer vs seller vs admin vs guest
- What makes this different from existing solutions (the real differentiator)
- The business model and monetization strategy
- Geographic and cultural context (regions, languages, currencies)
- What the user's life looks like before and after using this product
- What success looks like in 6 months, not just at launch
**Priority:** Critical — fix this before the next test.

---

## Issue 8 — Skills lack taste and visual quality standards
**Status:** 🔴 Open
**What happened:** The full-stack marketplace test produced a technically correct but visually generic, low-quality product. The code is production-grade but the actual output looks like a junior dev's first tutorial project — not a high-end elite product.
**Root cause:** The skills have elite engineering standards but no elite product standards. No taste layer. No visual opinion. No reference points for what premium actually looks like.
**Specifically missing:**
- UX Designer has no named premium references (Airbnb, Stripe, Linear, Shopify) and no opinion on what makes a marketplace feel high-end vs generic
- SWE-FE builds correctly but has no taste layer — no opinion on animations, micro-interactions, component quality, visual hierarchy, spacing
- PM doesn't ask "show me a reference of what you want this to feel like" or "what premium experience are you going for"
- Growth PM doesn't push for a differentiated, premium onboarding experience
- Content Designer doesn't ask about brand voice beyond basic tone
- No skill refuses to ship a generic-looking UI the way AppSec refuses to ship vulnerable code
**Impact:** Critical — this is the most visible failure. Users pay $39 for elite output. A generic-looking app destroys credibility immediately.
**Fix needed:** Add a taste layer to UX Designer, SWE-FE, PM, Growth PM, and Content Designer skills:
- Named premium references every skill must aspire to
- Specific refusals around generic UI patterns
- PM intake must ask for visual references and premium experience goals
- UX Designer must have opinions on what elite looks like, not just what's accessible
- SWE-FE must have standards for micro-interactions, animations, component quality
- A shared visual quality bar equivalent to ELITE_STANDARDS but for product quality
**Priority:** Critical — fix alongside Issue 7. Both affect output quality at the root.

---

## Upcoming fixes (in order)

1. **Issues 7 + 8 together** — deepen Leadership intake AND add taste/visual quality layer. Both are root-level output quality issues.
2. **Issue 5** — add live browser verification to the pipeline delivery step.
3. **Issue 1** — investigate parallel subagent execution.
4. **Issue 6 last** — plugin cache competition. Low priority.

---

## Full stack test results

### Test 1 — Simple auth API
- Prompt: "Build a simple user authentication system with login and signup endpoints"
- Result: Production-grade auth API, Node 20 + TypeScript strict, Fastify, PostgreSQL, Drizzle
- 38/38 tests passing
- Zero vulnerabilities
- All 5 stages gated correctly
- Staff Engineer had to be called explicitly (Issue 2/3 — now fixed)
- No CLAUDE.md produced (Issue 4 — now fixed)
- Parallel subagents didn't fire (Issue 1 — open)

### Test 2 — Full stack marketplace
- Prompt: "Build a full-stack marketplace app..." (no explicit skill call)
- Result: Full marketplace — auth, product listings, detail page, cart, REST API, React frontend, PostgreSQL, deployment config
- 13 backend tests + 16/16 live smoke tests passing
- Zero production vulnerabilities
- All 5 stages gated with recorded evidence
- Staff Engineer triggered automatically ✅
- CLAUDE.md produced ✅
- App not verified in browser (Issue 5 — open, Docker daemon wasn't running during pipeline)

---

## Next test — Full verification including browser

Once Issue 5 is fixed, run the same full-stack marketplace test and verify:
- App loads in browser at the expected URL
- User can sign up and log in
- Product listings show up
- Cart works
- All pages render correctly

*Issues Plan v1.1 — Updated after Test 2*

---

## Issue 9 — Pipeline structural redesign needed
**Status:** 🔴 Open
**What happened:** External review identified critical structural flaws in the pipeline stage assignments. Roles are in the wrong stages, causing downstream work to happen without the context it needs.

**Critical structural flaws:**

**Misplaced roles:**
- UX Designer, UXR, Content Designer, Design Ops are in Stage 4 (after Infrastructure) — WRONG. Engineers are building APIs and infrastructure without knowing what the UI looks like. Design must happen in Stage 1 before any engineering begins.
- MLOps is in Stage 5 (Data & Docs) — WRONG. MLOps is infrastructure for AI models. It belongs in Stage 3 alongside DevOps and SRE.
- Data Engineer is partially misplaced — needs a planning role in Stage 3 and execution role in Stage 5.

**Missing roles:**
- QA/Automation Engineer — no dedicated quality gate before security. Engineers write their own tests but no independent quality audit exists.

**The correct restructured pipeline:**
- Stage 1 — Leadership + Discovery: PM, Growth PM, EM, Tech Lead, CTO Advisor, UX Designer, UXR, Content Designer, Design Ops
- Stage 2 — Engineering: SWE-FE, SWE-BE, Mobile, AI/ML, API Integration, Cryptographic Eng
- Stage 3 — Infrastructure: DPE, Release Eng, SRE, DevOps, DBA, Cloud Architect, MLOps
- Stage 4 — Security + QA: AppSec, Red Team, SecOps, Compliance, Corp Security, QA/Automation Engineer
- Stage 5 — Data & Docs: Data Scientist, Data Engineer, Data Governance, Tech Writer, L10n

**What this changes:**
- 4 skills move stages (UX Designer, UXR, Content Designer, Design Ops → Stage 1)
- 1 skill moves stages (MLOps → Stage 3)
- 1 new skill added (QA/Automation Engineer → Stage 4)
- Total skills goes from 30 to 31 specialists
- Every affected SKILL.md collaboration protocol needs updating
- Staff Engineer routing logic needs updating
- DOCTRINE.md org chart needs updating
- Pipeline canvas needs full redraw
- Obsidian vault needs updating

**Impact:** Critical — this is a fundamental architectural flaw. Building without design context produces exactly the generic low-quality output we saw in Test 2.
**Priority:** Critical — fix before any more testing.

---

## Updated fix order

1. **Issue 9** — restructure the pipeline. Foundation everything else builds on.
2. **Issues 7 + 8** — deepen Leadership intake AND add taste/visual quality layer. Do after restructure since Stage 1 is changing.
3. **Issue 5** — add live browser verification to pipeline delivery.
4. **Issue 1** — investigate parallel subagent execution.
5. **Issue 6** — plugin cache competition. Low priority.

---

## Issue 10 — No design system or UI component library enforced
**Status:** 🔴 Open
**What happened:** The pipeline builds UI from scratch every time with no shared design system. SWE-FE builds whatever it decides — raw HTML, random component choices, inconsistent spacing and typography.
**Impact:** High — inconsistent UI feels amateur. Elite products have a consistent component library that carries across every screen.
**Fix needed:** SWE-FE and UX Designer skills must default to shadcn/ui + Tailwind with a defined design token system. No raw HTML for UI components. No custom components when a system component exists.
**Priority:** High.

---

## Issue 11 — No mobile-first enforcement
**Status:** 🔴 Open
**What happened:** The SWE-FE skill says mobile-first but in practice built a desktop-first layout in both tests.
**Impact:** High — most users are on mobile. A desktop-first layout fails the majority of real users immediately.
**Fix needed:** UX Designer and SWE-FE must have an explicit hard rule — mobile viewport is the primary canvas, desktop is the enhancement. The gate must check mobile layout before passing.
**Priority:** High.

---

## Issue 12 — No real-world reference mandate
**Status:** 🔴 Open
**What happened:** Design and frontend skills build in a vacuum with no named inspiration or reference points. Output defaults to generic because there's no premium target to aim at.
**Impact:** High — without references, "elite" has no definition. You can't build premium if you don't know what premium looks like.
**Fix needed:** Every design and frontend skill must name 2-3 premium reference products before writing a single line. Examples: Airbnb for marketplace flow, Stripe for payment UX, Linear for dashboard design, Shopify for seller experience. These must be explicit requirements, not suggestions.
**Priority:** High — directly causes Issue 8.

---

## Issue 13 — Staff Engineer has no taste gate
**Status:** 🔴 Open
**What happened:** The Staff Engineer's review gate checks for production-grade code but has no visual or UX quality check. It can pass a gate on an ugly, generic app as long as the code is correct.
**Impact:** Critical — the gate is supposed to be the final quality bar. If it doesn't check product quality, ugly ships.
**Fix needed:** Add a fourth gate question to the Staff Engineer: "Would a user pay for this experience?" If the answer is no — the gate fails. The Staff Engineer must evaluate visual quality, UX flow, and premium feel alongside code quality.
**Priority:** Critical.

---

## Issue 14 — No error state or empty state standards
**Status:** 🔴 Open
**What happened:** Both tests produced apps with no designed error states, no empty states, and no loading skeletons. Pages either work or show nothing.
**Impact:** High — empty and error states are where products feel cheap or premium. A blank screen on error destroys trust. A skeleton loader feels polished.
**Fix needed:** UX Designer skill must require error states, empty states, and loading states for every screen as a gate requirement. SWE-FE must implement loading skeletons by default. Content Designer must write error and empty state copy for every screen.
**Priority:** High.

---

## Issue 15 — No performance budget enforcement
**Status:** 🔴 Open
**What happened:** The SWE-FE skill mentions Core Web Vitals but nothing actually measures or enforces them during the pipeline run. Performance is aspirational, not gated.
**Impact:** High — a slow app feels cheap regardless of how good it looks. Elite frontend has hard budgets.
**Fix needed:** Add hard performance budgets to the SWE-FE gate criteria: LCP under 2.5s, CLS under 0.1, INP under 200ms. The pipeline must measure and report these before the Stage 2 gate passes. If budgets aren't met, the gate fails.
**Priority:** High.

---

## Updated fix order

1. **Issue 9** — restructure the pipeline stages. Foundation everything else builds on.
2. **Issues 7 + 8 + 12** — deepen Leadership intake, add taste layer, mandate real-world references. All root-level quality issues.
3. **Issue 13** — add taste gate to Staff Engineer. Makes the gate actually catch quality failures.
4. **Issues 10 + 11 + 14 + 15** — design system enforcement, mobile-first, error/empty states, performance budgets.
5. **Issue 5** — add live browser verification to pipeline delivery.
6. **Issue 1** — investigate parallel subagent execution.
7. **Issue 6** — plugin cache competition. Low priority.
