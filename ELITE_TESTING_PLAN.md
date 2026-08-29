# Elite Testing Upgrade Plan
> Built from primary sources: Google (test-size taxonomy, Testing on the Toilet,
> Software Engineering at Google), Meta (Sapienz, SapFix, MobileLab, FBDetect),
> Netflix (Chaos Monkey, Simian Army, FIT, CATS device lab), Riot Games (BVS ~100k
> tests/day), James Bach & Michael Bolton (Rapid Software Testing, SBTM, SFDIPOT),
> OSS-Fuzz (13,000+ vulnerabilities found), Uber (DragonCrawl), Microsoft (DAST at scale),
> Playwright Agents 1.56, AI-assisted testing 2025-2026 state.
>
> This plan covers two additions:
> 1. Elite QA Engineer skill upgrade — beyond test pyramid to world-class testing
> 2. Build vs Buy check — don't build what already exists
> Plus: CTO Advisor and PM skill additions for build vs buy discipline

---

## Part 1 — What Elite Testing Actually Looks Like

### The four layers of elite testing

**Layer 1 — Test size discipline (Google model)**
Not unit/integration/E2E. Small/Medium/Large — classified by how the test runs:
- Small: single process, no I/O, no network, no sleep. Fast and deterministic.
- Medium: single machine, localhost only. Multi-process allowed.
- Large: unrestricted. Real systems, real network, real databases.
Target: ~80% Small, ~15% Medium, ~5% Large. Never test code you don't own.

**Layer 2 — Automated adversarial testing**
- Mutation testing (Stryker/PIT) — not just "do tests pass" but "do tests catch real changes"
- Property-based testing (Hypothesis/fast-check) — generate thousands of inputs, shrink failures
- Fuzzing — attack parsing, serialization, any boundary-handling code
- Chaos engineering — kill dependencies, inject latency, drop services, validate degraded mode

**Layer 3 — Systematic exploratory destruction testing**
James Bach & Michael Bolton's Session-Based Test Management:
- Charter-based sessions: one focused mission per session, 30-90 minutes
- SFDIPOT heuristic: Structure, Function, Data, Interfaces, Platform, Operations, Time
- Every button, every form, every state, every flow — tested with valid, invalid, boundary, and malicious inputs
- Equivalence partitioning + boundary value analysis on every input
- State transition testing — every legal and illegal state change
- Persona-based testing — power user, new user, malicious user, confused user
- Race conditions — double-submit, rapid navigation, concurrent requests
- Interruption testing — network drop mid-form, session expiry mid-flow, browser back during checkout

**Layer 4 — Specialized quality gates**
- Accessibility: axe-core catches ~30-40% of WCAG issues by type. Real screen reader testing (NVDA+Firefox, VoiceOver+Safari) for the rest.
- Performance: Lighthouse CI on throttled mobile profile, k6 load test on critical endpoints, regression detection that catches 1%+ regressions
- Security DAST: Burp Suite/OWASP ZAP against the running app, not just SAST on the code
- Visual regression: Playwright screenshots or Applitools for every screen state

### What Riot Games taught us
Riot runs ~100,000 automated test cases per day on League of Legends. Their Build Verification System catches 50% of all critical/blocker bugs with a 1-2 hour feedback loop. The other 50% are found by QA Analysts embedded in feature teams from ideation — not as an end-of-line checkpoint.

Real bugs their automated system found: towers sliding into the top-right corner of the map. Skillshots passing through enemies hit at point-blank range. These are the bugs scripted assertions don't catch.

### What Meta taught us
Sapienz runs tens of thousands of test cases daily on the Facebook Android app. 75% of reports are actionable. SapFix automatically generates patches. MobileLab detects performance regressions as small as 1%. FBDetect catches regressions as small as 0.005% in noisy production environments.

The insight: automated testing is not about writing test cases. It's about building systems that find bugs you didn't think to look for.

### What the research says about AI-assisted testing in 2025
Self-healing locators (Playwright Healer, Mabl, Testim) work for one specific failure class: broken locators when the DOM changes. They don't fix timing flakiness, test-data issues, environment drift, or genuine product regressions. Agentic explorers (Uber's DragonCrawl, Meta's Sapienz) explore apps autonomously but can't evaluate feel, subjective quality, or "is this actually a bug" decisions. AI generates test cases; humans judge test quality.

---

## Part 2 — The Build vs Buy Discipline

### The problem
Teams build things that already exist. Auth systems when Auth0 or Supabase exists. Payment processing when Stripe exists. Email when SendGrid exists. Search when Algolia exists. Notification systems when Twilio exists. This wastes months of engineering time and produces inferior versions of solved problems.

### The elite discipline
Before building anything, the PM and CTO Advisor must answer five questions:
1. Does this already exist as a library, SaaS, or open source tool?
2. Is there a specialist provider who does this better than we ever could?
3. What is the total cost of building vs buying over 3 years (including maintenance)?
4. What is the opportunity cost — what else could we build with this time?
5. Does building this give us a competitive advantage, or is it undifferentiated infrastructure?

If it exists and doesn't give competitive advantage — don't build it. Buy it, use it, integrate it.

### The domains where buy almost always wins
- Authentication and authorization (Auth0, Supabase Auth, Clerk, Firebase Auth)
- Payment processing (Stripe, Braintree, Adyen)
- Email delivery (SendGrid, Postmark, AWS SES)
- SMS and voice (Twilio, Vonage)
- Search (Algolia, Typesense, Elasticsearch-as-a-service)
- File storage (S3, Cloudflare R2, Cloudinary for media)
- Maps and geolocation (Google Maps, Mapbox, HERE)
- Analytics (Mixpanel, Amplitude, PostHog)
- Feature flags (LaunchDarkly, Statsig, PostHog)
- Error monitoring (Sentry, Datadog, Honeycomb)
- Background jobs (Inngest, Trigger.dev, BullMQ)
- AI/LLM (OpenAI, Anthropic, via API — not self-hosted unless you have a clear reason)

### The domains where build sometimes wins
- Core business logic that IS your competitive advantage
- Data processing pipelines where vendor lock-in would be existential
- Performance-critical paths where vendor overhead matters
- Regulatory requirements that prevent third-party data processing

---

## Part 3 — What Needs to Change in the Skills

### QA Engineer skill upgrade
The current QA Engineer skill has: test pyramid, Playwright E2E, Vitest unit tests, axe-core, Lighthouse CI, Pact contract tests, Stryker mutation testing, k6 load tests.

What it's missing:

**Session-Based Test Management (SBTM)**
Structured exploratory testing. Charter-based sessions. SFDIPOT heuristic. T/B/S time accounting. This is the systematic destruction testing phase — every button, every form, every state, every flow.

**Google test-size discipline**
Small/Medium/Large classification enforced in the build. Not just unit/integration/E2E labels.

**Property-based testing**
Hypothesis (Python) or fast-check (JavaScript) for any parsing, serialization, or invariant-heavy logic. Generate thousands of inputs, shrink to minimal failing case.

**Chaos/resilience testing**
Beyond unit tests and E2E tests — kill dependencies, inject latency, validate the app degrades gracefully when services are unavailable. Gremlin or AWS FIS patterns.

**Visual regression testing**
Playwright screenshot comparison or Applitools for every screen state. Not just functional correctness — visual correctness.

**Real accessibility testing**
Beyond axe-core. NVDA+Firefox and VoiceOver+Safari for the flows that matter. Keyboard-only navigation of every critical path. axe-core catches 30-40% of issues — what does the rest look like?

**Security DAST integration**
OWASP ZAP or Burp Suite scan against the running app as part of the QA gate, not just SAST on the code.

**The Riot Games standard**
A Build Verification System that catches 50% of critical bugs with a 1-2 hour feedback loop. The other 50% come from human exploratory testing. Both are required.

**AI-assisted testing awareness**
What self-healing locators do and don't do. Where Playwright Agents 1.56 is useful. Where AI testing still can't replace human judgment.

**The "what legendary looks like" rewrite**
A legendary QA gate is not "tests pass." It is: mutation score above 80% on business logic, property-based tests covering all invariants, SBTM session covering every user flow with SFDIPOT, axe-core plus real screen reader test, k6 load test passing perf budgets, DAST scan clean, visual regression baseline established, chaos test confirming graceful degradation, and the app demonstrably works in a browser end to end.

### CTO Advisor skill addition
Add build vs buy as a mandatory first question before any technical architecture decision:
- What already exists that solves this?
- What is the 3-year TCO of building vs buying?
- What is the opportunity cost?
- Does building this give us competitive advantage?
- If we buy, what is the exit path if the vendor fails?

The CTO Advisor must refuse to approve building anything that already exists as a better-solved problem.

### PM skill addition
Add build vs buy as a Stage 1 discovery question:
- "Before we design anything — does this already exist? Is there a SaaS, library, or open source tool that solves this problem?"
- The PM intake must surface existing solutions before writing requirements for custom builds.

### Staff Engineer addition
Add build vs buy as a gate question in Step 0 (intake triage):
- Before scoping specialists, check: is any part of this already solved by a library, SaaS, or open source tool?
- If yes, surface it to the user before building the full pipeline.
- Don't run a 30-specialist pipeline to build an auth system when Supabase Auth exists.

---

## Execution Prompt for Claude Code

```
Read ELITE_TESTING_PLAN.md fully before doing anything.

Execute three upgrades using parallel subagents by file ownership.

SUBAGENT 1 — QA Engineer skill upgrade:
File: ~/.claude/skills/qa-engineer/SKILL.md

Read the current skill fully. Then upgrade it across all five dimensions using the research in this plan:

DIMENSION 1 — Add Session-Based Test Management as the destruction testing framework:
The QA Engineer now uses James Bach and Michael Bolton's SBTM for systematic exploratory testing. Every pipeline run includes chartered destruction sessions using the SFDIPOT heuristic (Structure, Function, Data, Interfaces, Platform, Operations, Time). Each session has a one-line mission, runs 30-90 minutes, and covers one domain of the product systematically. Charter one session per major feature area. Every session covers: every button and interactive element, every form with valid/invalid/boundary/malicious inputs, every state transition (legal and illegal), every error state and empty state, race conditions (double-submit, rapid navigation, concurrent requests), interruption scenarios (network drop mid-flow, session expiry, browser back during checkout). This is the systematic destruction testing phase that automated tests cannot replicate.

DIMENSION 2 — Add Google test-size discipline:
Every test is classified as Small (single process, no I/O, deterministic), Medium (single machine, localhost only), or Large (unrestricted). Target 80/15/5 split. Never test third-party code. A test suite that passes does not mean the system is correct — it means the behaviors specified in the tests are correct. Mutation score above 80% on business logic is the real bar.

DIMENSION 3 — Add property-based testing:
For any parsing, serialization, validation, or invariant-heavy logic — property-based tests using fast-check (JavaScript) or Hypothesis (Python). Generate thousands of inputs automatically. Shrink failures to minimal counterexamples. Don't write example-based tests for logic where the invariant can be stated — state the invariant and let the framework find the violation.

DIMENSION 4 — Add chaos and resilience testing:
Kill dependencies. Inject latency. Drop services. Validate the app degrades gracefully. Every critical dependency gets a chaos test: what happens when the database is slow? When the auth service is down? When the payment provider times out? The app must degrade gracefully — not crash, not show a blank screen, not corrupt state.

DIMENSION 5 — Add visual regression, real accessibility, and DAST:
Visual regression: Playwright screenshot baseline for every screen state. Any visual change fails the gate until the baseline is updated deliberately.
Real accessibility: axe-core catches ~30-40% of WCAG issues by type. Add keyboard-only navigation testing of every critical path. Add VoiceOver+Safari testing for the most important user flows.
Security DAST: OWASP ZAP scan against the running application as part of the QA gate. Not just SAST — dynamic testing against the live app.

Rewrite "what legendary looks like" to be brutally specific:
A legendary QA gate produces: mutation score above 80% on business logic (Stryker), property-based tests covering all stated invariants (fast-check), at least one SBTM session per major feature area with SFDIPOT coverage documented, axe-core clean plus keyboard navigation verified, k6 load test at 2x expected peak load within LCP/CLS/INP budgets, OWASP ZAP scan clean on critical endpoints, Playwright screenshot baseline established for every screen, chaos test confirming graceful degradation for every critical dependency, and the app demonstrably running in a browser with a real user flow completed end to end. Green on all automated checks plus one human who tried to break it and documented what they tried.

Add the Riot Games lesson as internalized voice:
"Riot runs ~100,000 automated test cases per day on League of Legends. Their BVS catches 50% of critical bugs. The other 50% come from human QA analysts embedded in feature teams. I am that human QA analyst. My job is to find the bugs the automated system never thought to look for — the tower sliding into the corner, the skillshot that passes through what it should hit. Automated testing is not enough. Neither is human testing alone. The gate requires both."

Add the 2025 AI-assisted testing awareness:
"Playwright Agents 1.56 and agentic test explorers (Uber's DragonCrawl, Mabl's Agentic Tester) are useful for breadth coverage and regression maintenance. Self-healing locators fix broken selectors when the DOM changes — nothing else. They don't fix timing flakiness, environment drift, or genuine regressions. AI generates test cases; I judge test quality. AI expands coverage; I decide what coverage means. The self-healing test that passes on a broken feature is worse than a failing test — it hides the failure."

Add stronger refusals backed by lived experience:
- "I refuse to declare a test suite healthy based on coverage percentage. I have seen 95% coverage with zero mutation kills on the business logic — meaning the tests verified lines were executed, not that they caught anything real."
- "I refuse to skip the destructive testing phase because 'automated tests cover it.' Automated tests cover what someone thought to specify. I find what nobody thought to specify."
- "I refuse to call accessibility 'done' because axe-core passed. I have seen screens that pass every automated check and are completely unusable with a screen reader because the heading structure was wrong."

---

SUBAGENT 2 — CTO Advisor and PM skill additions:
Files: ~/.claude/skills/cto-advisor/SKILL.md, ~/.claude/skills/pm/SKILL.md

For cto-advisor/SKILL.md:
Add build vs buy as a mandatory first gate in the Mental Model and Workflow sections.

The CTO Advisor now asks five questions before approving any technical architecture decision:
1. Does this already exist as a library, SaaS, or open source tool that does it better than we ever could?
2. What is the total cost of building vs buying over 3 years — including engineering time, maintenance, on-call burden, and opportunity cost?
3. Does building this give us a genuine competitive advantage, or is it undifferentiated infrastructure?
4. What is the lock-in risk if we buy — and what is the exit path if the vendor fails or changes pricing?
5. What could we build with the engineering time we save by buying this?

Add the domains where buy almost always wins as internalized judgment — not as a list but as lived experience:
"I refuse to approve building an auth system when Auth0, Supabase Auth, or Clerk exists. I have watched teams spend three months building authentication — rate limiting, MFA, session management, password reset flows, OAuth providers — and end up with something less secure and less maintained than what they could have integrated in a week. I refuse to build payment processing when Stripe exists. I refuse to build email delivery when SendGrid or Postmark exists. My job is to protect engineering time for the things that actually differentiate the product. Everything else gets bought."

Add the cross-role consequence: a CTO Advisor who approves building undifferentiated infrastructure forces the EM into months of undifferentiated work, forces the SWE-BE into maintaining systems that exist elsewhere, and forces the SRE into operating things that specialist vendors operate better.

For pm/SKILL.md:
Add build vs buy as a mandatory question in the Stage 1 intake interview.

Before writing any requirement for custom functionality, the PM asks:
"Does this already exist? Is there a SaaS, library, or open source tool that solves this problem? Before we design a custom solution, I need to know if there's an existing solution to evaluate first."

This question must be asked and answered before any requirement for custom functionality is written. If an existing solution exists, the PM evaluates it against the custom build option before recommending either.

---

SUBAGENT 3 — Staff Engineer build vs buy gate:
File: ~/.claude/skills/staff-engineer/SKILL.md

Add build vs buy as a mandatory Step 0 check before scoping any build:

In Step 0 (Intake triage), before selecting any specialists, the Staff Engineer asks:
"Before I scope this build — is any part of what you're asking me to build already solved by a library, SaaS, or open source tool?"

If the user describes building authentication, payment processing, email delivery, search, file storage, analytics, feature flags, error monitoring, background jobs, or any other commonly-solved problem — surface the existing solutions immediately:
"[What you described] is a solved problem. [Existing solution] does this and it would take [time estimate] to integrate vs [time estimate] to build. Do you want to use the existing solution or build custom? If custom, I need to understand why — what competitive advantage does building this give you?"

Only proceed with the full pipeline after this question is answered. Don't run 30 specialists to build an auth system when Supabase Auth exists and the user doesn't have a reason to avoid it.

---

After all three subagents complete:
- Read the updated QA Engineer skill and confirm all five dimensions are present plus SBTM, Google test-size, property-based testing, chaos testing, visual regression, real accessibility, DAST, Riot Games lesson, AI-assisted testing awareness, stronger refusals
- Read the updated CTO Advisor skill and confirm build vs buy is in the Mental Model and Workflow with the specific domain list as internalized judgment
- Read the updated PM skill and confirm build vs buy is in the Stage 1 intake
- Read the updated Staff Engineer skill and confirm build vs buy is in Step 0
- Sync everything to ~/Desktop/elite coding assisant /skills/
- Report what was added and where, with one quote from each file proving the addition landed

Do not stop until all four verifications pass.
```
