# Report: Hero / About repositioning + nav on inner pages

**Date:** 2026-09-21
**Plan:** ./plan.md

## Summary

Hero, About, and `_config.yml` occupation content no longer mention a thesis and
are repositioned around HV cable / offshore wind asset engineering across
development, execution and operation. The navbar (including the existing
Thesis link) now also renders on inner pages. Nothing has been pushed.

## Step results

- [x] 1. `index.markdown` — Done. Option A hero line, no thesis mention.
- [x] 2. `about.markdown` — Done. Paragraph 3 replaced; thesis link removed.
      Execution-phase wording (uprating, monitoring-system commissioning) is
      based on Joko's direct statement, not on the vault CV.
- [x] 3. `_config.yml` — Done. `occupation` subtitle changed; DLR bullet
      reworded; one new project bullet for uprating / monitoring-system
      commissioning. No other keys touched.
- [x] 4. `_layouts/page.html` — Done. Navbar included, wrapper with
      `padding-top: 5rem` for the fixed navbar.
- [x] 5. Re-read edited files — Done. Full `git diff` of all four files
      checked against the plan on 2026-09-21.
- [x] 6. Local Jekyll build — Done. `jekyll build` (Ruby 3.4.10 via rbenv) into
      a scratch dir succeeded; built `index`, `about`, `thesis/progress` contain
      no "Master's"/thesis-work wording. Verified in the browser at
      localhost:4000: navbar with Thesis link renders on `/about/` and
      `/thesis/progress/`, no overlap at desktop (5rem is fine) or mobile
      (375px, burger menu shown).
- [x] 7. Report written; no `git push`.

## Issues encountered

- Earlier statement that Thesis was "not in the nav" was wrong for the home
  page: `navbar.html` already had it. The real gap was that `page` layout
  pages (About, Thesis index) had no navbar at all.
- Standalone dated reports in `thesis/progress/*.html` have no front matter,
  so they still have no site nav. Not changed (out of scope).

## Open items for human review

- **Restart `jekyll serve`.** `_config.yml` is not hot-reloaded, so the running
  server at localhost:4000 still shows the old occupation subtitle
  ("Engineer | Geek | Analyst") and the old DLR bullet with the Master's thesis
  reference. The fresh build has the new values.
- Navbar overlap on inner pages checked and fine (see step 6).
- About paragraph 1 still says "digitalization specialist"; consider aligning
  with the new hero.
- Vault HVC CV has no execution-phase line yet (uprating, monitoring-system
  commissioning). Add if you want the CV and site to match.
- Confirm before push.
