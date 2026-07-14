---
name: create-spec-issues
description: This skill should be used after a kick-off interview has produced a confirmed spec (`.project/SPEC.md` for a new project, or a new `.project/SPEC-milestone-<###>-<slug>.md` for a milestone) and that spec's work needs to be broken into actionable issues. Trigger phrases include "create issues from this spec", "break this spec into tickets", "turn the spec into issues", "spec this out into work items", or whenever a freshly confirmed spec needs to be decomposed into implementable units of work.
---

# Create Spec Issues

Runs after kick-off produces a confirmed spec. Decomposes it into one issue per unit of work — does not implement anything.

## 1. Find the spec

Use the highest-numbered `.project/SPEC-milestone-<###>-*.md` if any exist, else `.project/SPEC.md`. Read it thoroughly — if a milestone spec is in play, also skim `.project/SPEC.md` for project vision and constraints not repeated in the milestone spec.

## 2. Require GitHub

Run `gh repo view` (requires a GitHub remote and a working `gh auth status`). Issues live on GitHub — there is no offline fallback.

- No GitHub repo yet: tell the user, and offer to create one (`gh repo create`) — ask for name and visibility, and only run it once they confirm.
- `gh` missing or unauthenticated: say exactly what's missing and stop.

## 3. Decompose into units of work

Identify every discrete unit of work in the spec — each feature, component, workflow step, or task it describes. Favor finer granularity over bundling: every action called for in the spec must map to its own issue.

## 4. Create issues

For each unit of work, first check `.project/Reports/` for a completion report matching its slug — if one exists, that work is already done; skip creating an issue for it.

Otherwise, each issue is a detailed, specific implementation prompt an AI coding agent could execute directly — not a summary. Include: what to build, the relevant context/constraints from the spec, and a bullet list of clear, checkable acceptance criteria.

Create each with `gh issue create --title "..." --body "..."`.

## 5. Verify completeness

Re-check the issues created against the units of work from Step 3 — every one must be represented by exactly one issue or an existing `.project/Reports/` completion report. Report the final list to the user, noting any skipped as already done.
