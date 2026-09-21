# Plan: Hero / About repositioning + nav on inner pages

**Date:** 2026-09-21
**Status:** In progress

## Objective

Reposition the public site around HV cable engineering, power systems,
mechanical, energy, cable monitoring, asset management and risk-based
maintenance across the development, execution and operation phases of offshore
wind farms. Remove any mention of Joko working on a thesis from page content
(the Thesis nav link and the thesis pages themselves stay). Make the Thesis nav
link available on every page, not only the home page.

## Research findings

- Source of facts: `despicable-mind/05-professional/cv/joko_pawitro_HVC.md`,
  plus Joko's direct statement (2026-09-21) that he is also working on the
  execution phase: uprating, and commissioning of a cable monitoring system.
- `Thesis` already exists in `_includes/navbar.html` (links to
  `/thesis/progress/`), rendered on the home page via `hero.html`.
- `_layouts/page.html` (used by `/about/` and `/thesis/progress/`) has no
  navbar, so those pages have no nav at all.
- `about.markdown` paragraph 3 mentions the Master's/thesis and links to
  `/thesis/progress/`. `_config.yml` DLR project bullet says "also the focus of
  my Master's thesis". `index.markdown` hero says "as my Master's thesis".
- No page mentions the degree itself apart from the thesis paragraph.

## Steps

- [ ] 1. `index.markdown` — replace hero line with Option A wording, no thesis mention.
- [ ] 2. `about.markdown` — replace paragraph 3 (Master's/thesis) with an
      expertise paragraph covering development, execution (uprating,
      monitoring-system commissioning) and operation; remove the thesis link.
- [ ] 3. `_config.yml` — set `occupation` subtitle; reword the DLR project
      bullet without the thesis reference; add uprating and monitoring-system
      commissioning project bullets. Do not touch `exclude:` or other keys.
- [ ] 4. `_layouts/page.html` — include `navbar.html` and add top spacing for
      the fixed navbar, so the Thesis link appears on About and Thesis pages.
- [ ] 5. Re-read every edited file to verify the result on disk.
- [ ] 6. Local `bundle exec jekyll build` (requires a shell on Joko's machine —
      mark Skipped if unavailable).
- [ ] 7. Write `report.md`. Stop. No `git push`.

## Out of scope

- Thesis pages under `thesis/progress/` (content, styling, dated reports).
- Vault CVs (they may keep thesis/degree wording).
- Phone number (never published), analytics, new social links, styling changes.

## Human decision points

- Hero wording: Option A used by default because none was picked; easy to swap.
- Spacing value for the fixed navbar on inner pages could not be checked
  visually; needs a look in the browser.
- Push to the live site only after Joko reads the report.
