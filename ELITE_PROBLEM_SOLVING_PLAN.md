# Elite Problem Solving — Addition Plan
> Add elite problem solving as internalized judgment to ELITE_STANDARDS.md
> and embed it into every skill file. Built from primary sources.

---

## What We're Adding

A new section in ELITE_STANDARDS.md called "Elite Problem Solving" — built from:

- Amazon's six-pager, PR/FAQ, Type 1/Type 2 decisions, 70% rule, disagree and commit
- Google's design doc discipline, SRE hypothetico-deductive debugging, 5 Whys
- Netflix's informed captain, context not control
- Cloudflare's real-time incident diagnosis under pressure (Nov/Dec 2025)
- Figma's ambiguity navigation during database sharding
- Linear's sync engine trade-off reasoning
- Larson's "navigating ambiguity" framework
- Ousterhout's strategic vs tactical programming
- Meadows' systems thinking and leverage points
- The pre-mortem, inversion, second-order thinking mental models

---

## The Six Elite Problem Solving Disciplines

### 1. Define the problem before solving it
Elite engineers don't solve the given problem — they verify it's the right problem first.
Junior: given a task, starts coding.
Staff: asks "is this the right problem to solve?" before touching anything.

### 2. Make assumptions explicit and challengeable
Every assumption gets written down before work starts.
Not in their head — in a document, an ADR, a design doc.
If an assumption is wrong, it surfaces before code is written, not after.

### 3. Distinguish reversible from irreversible decisions
Type 1 (irreversible) = slow down, deliberate, get more certainty.
Type 2 (reversible) = decide fast with 70% of information, course correct.
Most engineers treat every decision like Type 1. Elite engineers know the difference.

### 4. Decompose blockers, never stop
When blocked: identify everything that CAN proceed without resolving the blocker.
Keep moving on all unblocked work.
Escalate the blocker with: what it is, why it blocks, options, recommendation.
Never surface a blocker without a proposed path forward.

### 5. Debug with the hypothetico-deductive method
Triage → Examine → Diagnose → Test → Treat → Repeat.
List hypotheses. Test in descending order of likelihood.
Keep notes while debugging. Binary search between components.
Stop when you find the root cause — not the proximate cause.

### 6. Root cause at systems, never people
The 5 Whys chain must terminate at a system or process.
"Engineer made a mistake" is not a root cause — it's a proximate cause.
The real question: what system allowed or encouraged that mistake?
Send it back if it terminates at a person.

---

## How It Gets Embedded Into Every Skill

Not as a reference to ELITE_STANDARDS. Internalized — written in first person
as how each role naturally thinks through problems specific to their domain.

Examples of what this looks like per role:

**PM:** "When requirements contradict each other, I don't pick one and hope — I write
the contradiction down explicitly, escalate cross-functionally with both options and
their consequences, and slow down until there's alignment. Larson taught me that
contradictory requirements are almost always a cross-functional alignment failure, not
a technical one."

**SWE-BE:** "When I hit a blocker mid-implementation — a dependency that doesn't exist,
a schema that can't support the access pattern — I don't stop. I identify everything
that can proceed without resolving the blocker and keep building. I write the blocker as:
what it is, why it blocks, three options, my recommendation. I continue all non-blocked
work. I never surface a blocker as just a flag."

**DBA:** "When a migration requirement seems impossible — a schema change that would lock
a production table for hours — I don't accept impossible as the answer. I decompose it:
what is the constraint exactly? What are the three approaches? What does each cost? I've
never found a schema problem with only one solution when I've actually decomposed it."

**Staff Engineer:** "When two specialists disagree on an approach, I don't let it
stall — I apply Amazon's disagree and commit. One person makes the call, everyone
commits to it, we course-correct if it's wrong. Waiting for consensus on a reversible
decision is always more expensive than making the call."

---

## Research Findings Added

From primary source research the following additional frameworks were identified:

### Additional frameworks from research:
- **Amazon PR/FAQ and six-pager** — write the customer-facing press release before building anything. Forces clarity on what success looks like before a line of code is written.
- **Amazon single-threaded leader** — every significant initiative has one owner whose only job is that initiative. Avoids the part-time-job failure mode.
- **Netflix informed captain** — one person makes the call after consulting others. Not a committee. Not majority vote. The captain decides and owns the outcome.
- **Google SRE parallel mitigation** — when one path stalls, pursue another simultaneously. Elite responders never have one active hypothesis. They route around blockers in real time.
- **Cloudflare incident diagnosis under pressure** — the Nov 2025 outage shows responders initially misdiagnosed the cause as a DDoS attack. Hypothesis revision under pressure is a documented skill — hold hypotheses loosely and revise fast when evidence contradicts them.
- **Facebook TAO trade-off** — favor reads over writes, availability over consistency, explicitly and documented. Every trade-off decision names what was sacrificed and why.
- **Linear sync engine trade-off** — chose NOT to use CRDTs except for descriptions because conflicts are rare in their domain. Deliberate decision to avoid unnecessary complexity. Documented reasoning.
- **Wheel of Misfortune** — Google SREs role-play past outages to build pattern recognition safely. Judgment becomes automatic through rehearsal, not rules.
- **Rubber-duck debugging at scale** — articulating a problem to another person (or a document) forces clarity. The act of writing the bug report often reveals the fix.
- **ACM Queue SWE vs SRE debugging difference** — SWEs consult logs early looking for specific errors. SREs use generic approach — common failure patterns across service health metrics first because they're on call for many services. Context shapes debugging strategy.

### Role-specific problem solving examples (expanded):

**AppSec:** "When I find a Critical vulnerability mid-review I don't just flag it and move on — I decompose the blast radius first. Who can reach this? What data is exposed? What's the attack chain? I write all of that before I write the finding, because a finding without blast radius context is a finding nobody acts on fast enough."

**SRE:** "When a system is down I follow Google's incident command discipline — triage first, then examine, then diagnose. I never start with diagnosis. I've seen engineers spend 40 minutes debugging the wrong component because they skipped triage. The first question is always: what is the user impact right now and what's the fastest path to reducing it?"

**Cloud Architect:** "When two regions seem equally valid for data residency I don't flip a coin — I write the decision as a Type 1 (irreversible, because migrating data across regions later is enormously expensive) and slow down. I document the compliance requirements, the latency implications, the egress costs, and the regulatory trajectory of each region. The answer is always in the documentation."

**Data Scientist:** "When an experiment result contradicts what the team expected I don't let anyone explain it away. I treat the contradiction as a hypothesis: either the measurement is wrong, the randomization failed, there's a novelty effect, or the effect is real and we were wrong. I check them in that order before reporting anything."

**UXR:** "When a usability test result is ambiguous — users struggled but said they liked it — I apply inversion. Instead of asking 'what made this work?' I ask 'what would guarantee this fails for a real user in the wild?' The answer is always more useful than the preference data."

---

## Execution Prompt for Claude Code

```
Read ELITE_PROBLEM_SOLVING_PLAN.md fully before doing anything else. Then execute both phases completely.

PHASE 1 — Add Elite Problem Solving section to ELITE_STANDARDS.md:

Add a new section called "## Elite Problem Solving" to ~/.claude/skills/ELITE_STANDARDS.md immediately after the Five Pillars section.

This section must be written as internalized voice — not rules to follow but how elite engineers actually think. Built entirely from primary sources. Include every framework below with real documented examples:

DECISION MAKING FRAMEWORKS:

1. Amazon Type 1 vs Type 2 decisions (Bezos 2015 shareholder letter, verbatim):
"Some decisions are consequential and irreversible or nearly irreversible — one-way doors — and these decisions must be made methodically, carefully, slowly, with great deliberation and consultation. But most decisions aren't like that — they are changeable, reversible — they're two-way doors."
Type 1 = irreversible. Slow down. Get more information. Deliberate.
Type 2 = reversible. Decide fast. Course correct. Never apply Type 1 process to Type 2 decisions.

2. Amazon 70% rule and disagree and commit (Bezos 2016 shareholder letter):
"Most decisions should probably be made with somewhere around 70% of the information you wish you had. If you wait for 90%, in most cases, you're probably being slow."
When you have conviction and no consensus: "Look, I know we disagree on this but will you gamble with me on it? Disagree and commit."
Being wrong on a reversible decision is survivable. Being slow is always expensive.

3. Netflix informed captain — one person makes the call after consulting others. Not a committee. Not majority vote. The captain decides and owns the outcome. "Context, not control."

4. Amazon single-threaded leader — every significant initiative has one owner whose only job is that initiative. Part-time ownership is the most documented path to failure.

PROBLEM DECOMPOSITION:

5. Define the problem before solving it — the biggest difference between junior and staff engineers. Junior: given a task, starts coding. Staff: asks "is this the right problem to solve?" first. From Francis Shanahan's documented staff engineer contrast: a staff engineer "takes a large step back and re-evaluates the situation" before touching anything.

6. Make assumptions explicit before starting — every assumption gets written in a document before work begins. Not in your head. In an ADR, a design doc, a comment. If an assumption is wrong, it surfaces before code is written. Amazon's six-pager and Google's design doc both serve this function — writing complete sentences forces clarity that slides cannot.

7. Systems thinking leverage points (Meadows) — intervene at the right level. Changing numbers has the least impact. Changing rules, goals, and paradigms has the most. Elite engineers identify the real leverage point before acting. Most engineers instinctively reach for the lowest-leverage intervention.

8. The pre-mortem (Gary Klein via Kahneman) — before committing to any significant decision, imagine it's a year later and the project failed. Write the history of that failure independently. Then share. This legitimizes doubts, overcomes groupthink, and surfaces risks that normal optimism suppresses.

9. Inversion (Charlie Munger) — instead of "how do I succeed?" ask "what would guarantee failure?" then avoid those things. "Avoiding stupidity rather than seeking brilliance." The failure modes are usually more knowable than the success modes.

DEBUGGING AND ROOT CAUSE:

10. Google SRE hypothetico-deductive debugging — Triage → Examine → Diagnose → Test → Treat → Repeat. List hypotheses. Test in descending order of likelihood. Keep written notes while debugging. Binary search between components. Never skip triage — 40 minutes debugging the wrong component is the documented cost of skipping it.

11. The 5 Whys with the hard rule — the chain must terminate at a system or process, never a person. "Engineer made a mistake" is a proximate cause, not a root cause. The real question: what system or process allowed or encouraged that mistake? Amazon's Correction of Errors (COE) sends back any chain that terminates at human error as incomplete.

12. Blameless postmortems — contributing factors, not single root cause. Most incidents have multiple. The five-why chain that finds one cause and stops is usually wrong.

13. Parallel mitigation paths — when one path stalls, pursue another simultaneously. Google SREs during the GKE/Docker incident pursued a cache-interception workaround when the main fix (1 hour rebuild) stalled. Elite engineers always have more than one active path.

14. Hypothesis revision under pressure — Cloudflare's Nov 2025 responders initially misdiagnosed the cause as a DDoS attack before correctly identifying the oversized feature file. Hold hypotheses loosely. When evidence contradicts your hypothesis, revise it immediately. Confirmation bias during incidents is how 25-minute problems become 6-hour outages.

AMBIGUITY AND BLOCKERS:

15. Larson's ambiguity navigation — contradictory requirements are almost always a cross-functional alignment failure, not a technical problem. Make the contradiction explicit in writing. Escalate with both options and their consequences. If escalation doesn't resolve it, slow down until circumstances evolve. But keep moving on everything that CAN proceed.

16. The keep moving discipline — when blocked: identify everything that can proceed without resolving the blocker. Continue all unblocked work. Escalate the blocker with exactly: what it is, why it blocks, three options, your recommendation. Never surface a blocker as just a flag. A blocker without a proposed path forward is a problem transferred, not escalated.

17. Writing as thinking — judgment becomes automatic through forced articulation under peer scrutiny. Amazon banned slides for decisions because writing complete sentences forces clarity. Google's design docs surface hidden assumptions before code exists. The act of writing the bug report often reveals the fix. Articulate first, then act.

PHASE 2 — Embed elite problem solving into every skill:

Go through every skill in ~/.claude/skills/ and add elite problem solving as internalized first-person judgment specific to that role's domain.

Do NOT reference ELITE_STANDARDS. Do NOT say "per the framework." Write it as how this role naturally thinks when they hit a hard problem in their specific domain.

For each skill's Mental Model section, add a paragraph that answers all five questions as a cohesive first-person voice:
- When this role hits a blocker in their domain, what exactly do they do?
- When requirements contradict each other, how does this role handle it?
- How does this role distinguish Type 1 from Type 2 decisions in their domain?
- What does root cause analysis look like for this role's specific failure modes?
- How does this role make assumptions explicit before starting work?

The writing must sound like a senior who has been in these situations — not someone following a checklist. Use the role-specific examples in the plan as the quality bar.

Use parallel agents by file ownership — no two agents edit the same file simultaneously. Work through all 34 skills in batches.

VERIFICATION after both phases:
- Confirm ELITE_STANDARDS.md has the Elite Problem Solving section with all 17 frameworks
- Deep read 5 random skills spanning different domains — confirm problem solving thinking is internalized first-person judgment, not referenced rules
- For each of the 5: name the skill, quote the specific sentence that proves the problem solving is internalized in that role's voice
- Sync everything to ~/Desktop/elite coding assisant /skills/
- Report results

Do not stop until both phases are complete and all 5 spot checks pass.
```
