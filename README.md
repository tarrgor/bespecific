# bespecific

A set of [Claude Code](https://claude.com/claude-code) skills that implement a **spec-driven development** workflow: turn a rough idea into a confirmed spec, break it into issues, implement and review each one, and keep a running log of decisions and knowledge — all with you in the loop for every decision that matters.

## The workflow

```
kick-off ──────────────► create-spec-issues ──────────────► implement-issue
(idea → SPEC.md)         (SPEC.md → GitHub issues)          (issue → PR)
                                                                   │
                                                                   ▼
project-meeting  ◄────────────  merge-pr  ◄──────────  verify-implementation
(triage findings,               (approved PR             (PR → review comments)
 plan next steps)                → develop)                    │
        ▲                                                       ▼
        │                                              check-pr-comments
        └──────────── new issues, spec changes ◄────── (feedback → fixes)
```

1. **kick-off** — interviews you about a new project or milestone, one question at a time, and writes a confirmed spec.
2. **create-spec-issues** — reads the newest spec and breaks it into one GitHub issue per unit of work (or a markdown ticket if GitHub isn't available).
3. **implement-issue** — implements a single issue end to end: branch, code, tests, and a pull request.
4. **verify-implementation** — independently reviews the resulting PR for bugs, security issues, and unmet acceptance criteria, and comments on it.
5. **check-pr-comments** — triages review feedback on an already-implemented issue and fixes what's valid.
6. **merge-pr** — merges an approved PR back into `develop` and cleans up the branch.
7. **project-meeting** — a recurring status meeting: reviews open findings, reports on finished work, and plans what's next — always with your confirmation before anything is decided.

## The `.project/` directory

Skills read and write project state here (created automatically on first use):

| Folder | Purpose |
|---|---|
| `SPEC.md` | The original, confirmed project spec |
| `Tickets/` | Milestone specs and markdown-fallback issue tickets |
| `Reports/` | Short completion reports, one per finished issue |
| `Inbox/` | Findings surfaced during implementation, awaiting discussion |
| `Archive/` | Resolved findings and past meeting records |
| `Knowledge/` | Durable learnings, organized by topic |
| `Branding/Assets/` | Brand and design assets |

## How to use it

Skills live in a plain top-level `skills/` folder rather than `.claude/skills/`, so Claude Code won't auto-discover them as slash commands. Instead, just tell Claude what you want in plain language — e.g. *"kick off this project"*, *"implement issue #12"*, *"let's have a project meeting"* — and point it at the relevant `skills/<name>/SKILL.md` if it doesn't pick it up on its own.

## Contributing skills

New skills go in `skills/<name>/SKILL.md`. Per [CLAUDE.md](CLAUDE.md), keep them brief and precise — every sentence should earn its tokens.
