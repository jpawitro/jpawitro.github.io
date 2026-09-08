# RPI workflow (Research → Plan → Implement → Report)

This folder holds dated task packages for any AI-executed change to this repo
that's more than a single trivial edit. See `AGENTS.md` at repo root for the
mandatory rules — this README just documents the folder convention.

## Structure

```
rpi/
├── README.md                              <- this file
└── <YYYY-MM-DD>_<short-slug>/
    ├── plan.md                            <- written before execution
    └── report.md                          <- written after execution
```

One folder per task. Date is the day the plan was written. Slug is a short
kebab-case description (e.g. `site-content-and-nav-refresh`).

## plan.md template

```markdown
# Plan: <title>

**Date:** YYYY-MM-DD
**Status:** Not started / In progress / Done / Blocked

## Objective

One or two sentences on what this achieves and why.

## Steps

- [ ] Step 1 — description
- [ ] Step 2 — description
- [ ] ⚠️ Step N — description (DESTRUCTIVE / IRREVERSIBLE — requires explicit
      human confirmation before running)

## Out of scope

What this plan deliberately does not touch.

## Human decision points

Anything the AI cannot decide alone (e.g. "publish phone number or not").
```

## report.md template

```markdown
# Report: <title>

**Date:** YYYY-MM-DD
**Plan:** ./plan.md

## Summary

One or two sentences on the outcome.

## Step results

- [x] Step 1 — Done. <notes>
- [x] Step 2 — Done. <notes>
- [ ] Step N — **Not done.** Reason: <why — e.g. "blocked on human confirmation">

## Issues encountered

Anything unexpected, errors, or judgment calls made mid-execution.

## Open items for human review

What the human should check or decide before the next step proceeds.
```

## Rule for AI assistants

Never combine plan and execution in one pass without the plan file existing on
disk first. Never mark a step "Done" in the report if it wasn't actually run —
mark it "Skipped" or "Not done" with a reason instead. The report is read by a
human afterward as the sole record of what happened; it must be accurate even
when the news is "I didn't finish this."
