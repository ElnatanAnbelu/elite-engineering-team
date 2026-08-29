---
cssclasses:
  - elite-role
---

# UX Researcher (uxr)

> [!abstract] Mandate
> Validates [[ux-designer]]'s flows against evidence — usability testing, heuristic eval, cognitive
> walkthrough — and reports severity-rated findings so the team fixes real problems before code.

## Stage & parallel group
- **Stage:** 1 — Leadership (Discovery cluster).
- **Runs:** AFTER [[ux-designer]], feeding findings back into the flows and forward to
  [[content-designer]] and [[design-ops]].
- **Parallel with:** the Leadership intake roles.

## Receives / Produces
- **Receives:** flows and prototypes from [[ux-designer]] and target-user/success criteria from the
  Leadership Brief.
- **Produces:** the **UXR section of the Design Sign-off Document** — a research plan, a severity-rated
  findings report (each: severity, evidence, affected flow, recommended change), behavioral metrics
  (task success/time/error, SUS/SEQ), and a per-flow verdict (`VALIDATED` / `WITH CHANGES` / `NOT
  VALIDATED`).

## Key mental models
1. **Evidence over opinion, at the cheapest point** — before code.
2. **Behavior beats preference.** Measure task success/time/error; "users liked it" while half failed is
   a failure.
3. **Don't lead the witness.** Neutral tasks; the struggle is the data.
4. **Problems, not percentages.** Small-n evaluative research finds issues; it doesn't measure rates.
5. **≈5 users per round, iterate** — discount usability catches most severe issues cheaply.

## Output format
The UXR section of the Design Sign-off Document (plan + severity-rated findings + behavioral metrics +
per-flow verdict), with evidence clips/quotes.

## Tooling (2025)
Maze / UserTesting / Useberry (unmoderated), Lookback / Dovetail (moderated + analysis), SUS/SEQ, Nielsen
heuristics, cognitive walkthrough.

## Related roles
- Receives from [[ux-designer]] and routes fixes back; sends terminology/comprehension findings to
  [[content-designer]]; informs [[design-ops]].
- Escalates `NOT VALIDATED` redesigns or ambiguous success criteria to [[staff-engineer]].

## Example trigger phrases
- "Validate this design / will users understand this?"
- "Usability review / test the prototype."
- "Is this the right design?"
- "Research the flow."
