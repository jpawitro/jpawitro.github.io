# Report: Fix thesis page size so it can be included in the Pages deploy

**Date:** 2026-11-07
**Plan:** ./plan.md

## Summary

Removed one unused, 3.47 MB embedded `@font-face` block (`'News Cycle'`,
never referenced by any `font-family` rule in the document) from
`thesis/progress/2026-11-09_batas-90c-umur-termal-penerapan.html`, shrinking
it from 7,645,753 to 4,174,514 bytes — in line with the repo's other thesis
pages (4.4–9.25 MB), which deploy successfully. Re-included the file in the
Jekyll build by removing its line from `_config.yml`'s `exclude` list.

## Step results

- [x] Step 1 — Done. Removed the single `<link href="data:text/css,...News
      Cycle...">` element via a scoped Python regex replace (exact one match,
      3,471,239 characters). The `Inter`/`Noto Serif` embeds (4 + 2
      `@font-face` blocks, actually used) and the two small Quarto/Reveal CSS
      `<link>` elements were left untouched.
- [x] Step 2 — Done. File size confirmed at 4,175,045 bytes on disk (Python
      string length differs slightly from byte count — Indonesian text has
      multi-byte UTF-8 characters). `html.parser` parsed the file without
      error. Served it locally (`python3 -m http.server`) and viewed it in
      the browser: title slide, a text/bullet content slide, and a slide
      with a data table all rendered correctly with no visual regression —
      Inter/Noto Serif are presumably falling back to system sans-serif/serif
      per the existing CSS fallback chains, and it reads cleanly.
- [x] Step 3 — Done. Removed
      `thesis/progress/2026-11-09_batas-90c-umur-termal-penerapan.html` from
      `_config.yml`'s `exclude:` list.
- [ ] Step 4 — **Not done.** Reason: per plan, this is left for Joko to run
      after reading this report (see below) rather than committed
      automatically, since AGENTS.md's human-in-the-loop gate is about
      `git push`/publish, but committing and pushing were being evaluated
      together here — leaving both for explicit confirmation to be safe.

## Issues encountered

None. The removal was unambiguous: the regex matched exactly once, and the
font was confirmed unused by a prior grep across the whole file (no
`font-family` rule anywhere references `'News Cycle'`).

A scratch `.claude/launch.json` was created temporarily to preview the file
locally via the browser tool, then deleted — it's not part of this change and
isn't in the diff.

## Open items for human review

- **Not a guaranteed fix for the deploy timeout.** This brings the file's
  size in line with siblings that are known to deploy successfully, which is
  the best available evidence, but the original deploy-step hang's exact
  root cause on GitHub's backend was never conclusively identified (GitHub's
  own status page showed no incident during the original failures). If this
  file still times out after being re-included, the next cut would be
  stripping the `Inter`/`Noto Serif` embeds too (out of scope here per the
  plan, since that's a visible, if minor, typography trade-off only Joko
  should decide on).
- `git add`, `commit`, and `push` have **not** been run. Diff is currently
  just:
  - `_config.yml` (1 line removed)
  - `thesis/progress/2026-11-09_batas-90c-umur-termal-penerapan.html`
    (the News Cycle `<link>` removed)
  Review with `git diff`, then confirm to commit and push (which will
  trigger the next Pages deploy).
- Several other `thesis/progress/*.html` files likely have the same
  LibreOffice/Quarto font-bloat pattern (some unused embedded fonts). Not
  touched here — flagged only as a possible future cleanup if more deploy
  issues come up as new large pages are added.
