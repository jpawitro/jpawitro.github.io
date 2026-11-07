# Plan: Fix thesis page size so it can be included in the Pages deploy

**Date:** 2026-11-07
**Status:** Not started

## Objective

`thesis/progress/2026-11-09_batas-90c-umur-termal-penerapan.html` was excluded
from the Jekyll build (via `_config.yml`) by a Copilot PR
(jpawitro/jpawitro.github.io#2) as an emergency fix for repeated GitHub Pages
deploy timeouts. Joko wants this page actually published. This plan shrinks
the file enough to bring it back in line with the repo's other thesis pages
and re-includes it in the build.

## Research findings

- The file is a Quarto/Reveal.js slide export, 7,645,753 bytes.
- 6,438,048 bytes (~84%) is three embedded items:
  - A single `<link href="data:text/css,...">` element, 3,471,238 bytes,
    containing an `@font-face` for `'News Cycle'` as a base64 TTF.
    **Confirmed unused**: no `font-family` rule anywhere else in the document
    references `'News Cycle'`. This is dead weight from the export tool.
  - Six `@font-face` blocks in a `<style>` tag (~2,966,810 bytes total) for
    `'Inter'` and `'Noto Serif'`, which ARE used in the document's `.reveal`
    styles — but every usage already has a fallback chain (e.g. `"Inter",
    "Helvetica Neue", Arial, sans-serif` / `"Noto Serif", Georgia, serif`).
- The repo's other thesis/progress files are already 4.4–9.25 MB each and
  deploy successfully (confirmed via `gh run list`: the commit that added the
  similarly-sized `2026-11-02_batas-90c-risiko-anggaran-penuaan.html`,
  7,644,505 bytes, deployed fine in 1m16s). Removing just the unused
  News Cycle block brings this file to ~4.17 MB — inside that proven-working
  range — without touching anything actually rendered.

## Steps

- [ ] Step 1 — Remove the single unused `<link href="data:text/css,...News
      Cycle...">` element from
      `thesis/progress/2026-11-09_batas-90c-umur-termal-penerapan.html`
      via a scoped script (the line is too long to hand-edit). Leave the
      `Inter`/`Noto Serif` embeds and the two small Quarto/Reveal CSS
      `<link>` elements untouched.
- [ ] Step 2 — Verify resulting file size and spot-check the file still opens
      correctly in a browser (no broken HTML structure from the removal).
- [ ] Step 3 — Remove the `thesis/progress/2026-11-09_batas-90c-umur-termal-penerapan.html`
      line from `_config.yml`'s `exclude` list.
- [ ] Step 4 — Commit the two changes locally with a clear message.
      **Do not push** — per AGENTS.md, push happens only after Joko reads the
      report and confirms.

## Out of scope

- Touching any other thesis/progress file (several share the same bloat
  pattern but are already deploying fine; not this task's problem to fix).
- Stripping the `Inter`/`Noto Serif` font embeds — they're actually used, and
  removing them would be a visible (if minor) typography change, which is a
  judgment call for Joko, not an automatic cleanup.
- Any change to `about.markdown`, `index.markdown`, or `_config.yml`'s
  `occupations` list.

## Human decision points

- Whether ~4.17 MB is enough headroom, or Joko also wants the `Inter`/`Noto
  Serif` embeds stripped (fallback fonts) for more margin — flagged in the
  report, not decided here.
- Confirming before `git push` / live publish, per AGENTS.md's
  human-in-the-loop gate.
