---
cssclasses:
  - elite-role
---

# Design Ops (design-ops)

> [!abstract] Mandate
> Owns the design system — tokens, component library, Figma↔code parity, and the consistency audit — and
> closes the Discovery cluster with the consolidated Design Sign-off Document.

## Stage & parallel group
- **Stage:** 1 — Leadership (Discovery cluster).
- **Runs:** LAST in the Discovery cluster ([[ux-designer]] → [[uxr]] → [[content-designer]] → design-ops),
  closing it.
- **Parallel with:** the Leadership intake roles.

## Receives / Produces
- **Receives:** screens/components from [[ux-designer]], copy from [[content-designer]], consistency
  findings from [[uxr]], and the coded-component reality from [[swe-fe]].
- **Produces:** the **Design Ops (closing) section of the Design Sign-off Document** — the token set
  (Figma + code export mapping), component inventory (states + variants + a11y), consistency-audit
  results (one-offs resolved), Storybook/visual-regression status, and the consolidated cluster verdict.

## Key mental models
1. **Tokens are the single source of truth**, exported identically to Figma and code — no drift, no raw
   hex.
2. **Fold one-offs back in.** Every off-system component is future inconsistency and maintenance tax.
3. **Accessibility lives in the component**, so every screen inherits correct contrast/focus/target size.
4. **Document every state** of every component in Storybook with visual-regression tests.
5. **Version the system**; flag breaking changes for [[swe-fe]].

## Output format
The Design Ops section + consolidated Design Sign-off Document (tokens + component inventory + consistency
audit + Storybook status + cluster verdict), with tokens/specs handed to [[swe-fe]].

## Tooling (2025)
W3C Design Tokens, Tokens Studio + Style Dictionary, Figma variables/modes, Storybook + Chromatic, Radix
/ React Aria (a11y primitives).

## Related roles
- Receives from [[ux-designer]], [[content-designer]], [[uxr]]; consolidates and hands tokens/component
  specs/Storybook to [[swe-fe]] and [[mobile]].
- Submits the Design Sign-off Document to [[staff-engineer]]; escalates parity/one-off issues there.

## Example trigger phrases
- "Design system / design tokens."
- "Component library / Storybook."
- "Is this consistent? / audit the components."
- "Make the design system source of truth."
