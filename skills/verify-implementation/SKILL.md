---
name: verify-implementation
description: This skill should be used to review a pull request produced by implement-issue. Trigger phrases include "review this PR", "verify the implementation", "check PR #12", "review issue #12's implementation", or whenever a finished implementation needs an independent review before merge.
---

# Verify Implementation

Reviews a finished implementation against its issue — does not implement or fix anything.

## 1. Identify the issue and its PR

- Identify the GitHub issue by number. If genuinely unclear, ask.
- Find the PR whose head branch is `issue/<issue-number>-*` (`gh pr list --search "head:issue/<issue-number>-"`, or `gh pr view <number>` if the PR number is already known). Read the linked issue in full.
- Note the acceptance criteria specifically — they're the review's checklist.

## 2. Gather the diff

- `gh pr diff <number>`.
- Read every changed file's surrounding context, not just the diff hunks, before judging correctness.

## 3. Review

Check the diff from three angles:

- **Acceptance criteria** — does the change satisfy every criterion from the issue? Note any unmet or partially met.
- **Correctness** — logic errors, edge cases, regressions, missing or inadequate tests for the behavior change.
- **Security** — injection, auth/authorization gaps, unsafe deserialization, committed secrets, unvalidated input, unsafe defaults, and other OWASP-class flaws.

Report only concrete, verifiable findings — not stylistic preference.

## 4. Report findings

- Post each finding as a PR comment (`gh pr comment <number> --body "..."`, or an inline review comment via `gh api` when it ties to a specific line). Reference the acceptance criterion or line it relates to.
- No findings: post a short note that the review passed, stating which criteria were checked.
