# Fix Plan — Post-Testing Issues
> Hand this to Claude Code. Fix all 4 issues in order. Do not stop until all 4 are resolved and verified.

---

## Issue 1 — Task tool / parallel subagents not firing

**Problem:** The Staff Engineer tried to spawn parallel subagents via the Task tool and got "invalid tool parameters." It adapted and ran sequentially, which worked, but parallel execution is the designed behavior.

**Fix:** Add an explicit fallback protocol to `~/.claude/skills/staff-engineer/SKILL.md`. 

In the Workflow section, after Step 1, add this block:

```markdown
### Parallel execution protocol
Attempt to spawn each stage's agents in parallel via the Task tool. If the Task tool returns an error or is unavailable, immediately fall back to sequential execution — same doctrine, same gates, same quality bar. Never stop or ask the user about this. The fallback is silent and automatic. Sequential execution under DOCTRINE produces identical output quality to parallel; the only difference is wall-clock time.
```

This makes the fallback explicit and documented so it always behaves correctly regardless of environment.

**Verify:** Open `~/.claude/skills/staff-engineer/SKILL.md` and confirm the parallel execution protocol block is present in the Workflow section.

---

## Issue 2 & 3 — 513 competing skills causing trigger noise + having to explicitly call staff-engineer

**Problem:** `~/.claude/skills/` has 513 SKILL.md files from previous installs. Claude Code grabbed the Superpowers skill instead of the Staff Engineer on the first attempt. Users had to explicitly say "use the staff-engineer skill" — which is not acceptable for a product.

**Fix:** Clean up `~/.claude/skills/` so only the elite team lives there.

Step 1 — List everything currently in `~/.claude/skills/` that is NOT part of the elite team:
```bash
ls ~/.claude/skills/ | grep -v -E "^(ai-ml|api-integration|appsec|cloud-architect|compliance|content-designer|corp-sec|cto-advisor|data-engineer|data-governance|data-scientist|design-ops|devops|dba|dpe|em|growth-pm|l10n|mobile|mlops|pm|red-team|release-eng|sre|secops|swe-be|swe-fe|tech-lead|tech-writer|ux-designer|uxr|cryptographic-eng|staff-engineer|DOCTRINE.md|ELITE_STANDARDS.md)$"
```

Step 2 — Back up everything that is not the elite team:
```bash
mkdir -p ~/claude-skills-backup && \
ls ~/.claude/skills/ | grep -v -E "^(ai-ml|api-integration|appsec|cloud-architect|compliance|content-designer|corp-sec|cto-advisor|data-engineer|data-governance|data-scientist|design-ops|devops|dba|dpe|em|growth-pm|l10n|mobile|mlops|pm|red-team|release-eng|sre|secops|swe-be|swe-fe|tech-lead|tech-writer|ux-designer|uxr|cryptographic-eng|staff-engineer|DOCTRINE.md|ELITE_STANDARDS.md)$" | \
xargs -I{} mv ~/.claude/skills/{} ~/claude-skills-backup/
```

Step 3 — Verify only elite team remains:
```bash
ls ~/.claude/skills/ | wc -l
```
Should be 33 skill folders + DOCTRINE.md + ELITE_STANDARDS.md = 35 items total.

Step 4 — Verify Staff Engineer is there:
```bash
ls ~/.claude/skills/staff-engineer/SKILL.md
```

**Result:** When Claude Code starts, the only skills available are the elite team. The Staff Engineer will trigger automatically on phrases like "build", "ship", "take this to production" without any explicit calling.

---

## Issue 4 — No session context persistence between terminals

**Problem:** Closing the terminal loses all project context. A new session has to re-discover everything from scratch — re-reading files, checking ports, re-understanding the project.

**Fix:** Add a step to the Staff Engineer's final gate (Step 7) that writes a `CLAUDE.md` file to the project root at the end of every pipeline run.

In `~/.claude/skills/staff-engineer/SKILL.md`, update Step 7 — Final gate + delivery to include:

```markdown
### Session summary (write at end of every pipeline run)
After the final gate passes, write a CLAUDE.md file to the project root containing:
- What was built (one paragraph)
- The tech stack (language, framework, database, deployment)
- The key architectural decisions made and why
- Where everything lives (file structure summary)
- How to run it locally (exact commands)
- Any open items or known limitations
- The stage gate records summary

This file is read by Claude Code at the start of every new session in this project folder, giving instant context without re-discovery. Format it as a concise technical brief, not a tutorial.
```

**Verify:** After the next pipeline run, confirm a `CLAUDE.md` file exists in the project root with the correct content.

---

## Verification checklist — all 4 issues resolved when:

- [ ] Staff Engineer SKILL.md contains the parallel execution fallback protocol
- [ ] `~/.claude/skills/` contains only 35 items (33 skills + 2 doctrine files)
- [ ] Triggering Claude Code with "build X" activates staff-engineer automatically without explicit calling
- [ ] Every pipeline run produces a CLAUDE.md in the project root

---

## After all 4 fixes are verified — run the full stack test

Give Claude Code this prompt:

```
Build a full-stack marketplace app with:
- User authentication (signup, login, logout)
- Product listing page (sellers can post items)
- Product detail page
- Simple cart (add/remove items)
- REST API backend
- React frontend
- PostgreSQL database
- Full deployment config

Take this from idea to production. Use the staff-engineer skill.
```

This exercises every stage and every cluster — Leadership, Engineering (FE + BE + Mobile patterns), Infrastructure, Security, Design, and Data & Docs. Report back with the full pipeline output.

---

*Fix Plan v1.0 — Execute in order, verify each fix before moving to the next, do not stop until all 4 are resolved.*
