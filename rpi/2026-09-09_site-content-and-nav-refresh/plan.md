# Plan: Content, occupations, and navigation refresh

**Date:** 2026-09-09
**Status:** Not started

## Objective

Bring the site's content back in line with Joko's actual current profile
(HV Cable Specialist at Ørsted, MSc candidate, ~15 years engineering
background) and make the two real artifacts already sitting in the repo
(`thesis/progress/`, `quiz/`) actually reachable from the site, without
touching the underlying stack (Jekyll + Bulma + GitHub Pages stays as-is —
see `AGENTS.md` §4).

## Research (recon already done — 2026-09-09)

- `about.markdown` is unedited Jekyll/Minima boilerplate — never customized.
- `index.markdown` tagline is generic and doesn't mention the current
  specialization, thesis, or platform-building angle.
- `_config.yml` → `occupations` has only Ørsted (titled "Cable Monitoring
  Specialist" — that was the Feb'23–Jan'24 role; current per
  `despicable-mind/05-professional/cv/joko_pawitro_HVC.md` is "Cable
  Specialist, Export Cable Systems," May 2025–present) and Practicum. Elnusa
  (2011–2018, the asset-integrity/mechanical base) and the CTO/consulting
  stretch (2018–2022) are missing entirely, which erases the "how did a
  mechanical engineer end up doing subsea cable thermal modeling" throughline.
- `_includes/highlights.html` is Lorem Ipsum, currently commented out in
  `_layouts/home.html`.
- `_includes/navbar.html` has all nav links commented out — no working
  navigation exists.
- `thesis/progress/2026-09-07_data-cuaca-power-curve-model-wind-to-load.html`
  and `quiz/cohort_04_ind.html` exist in the repo but are linked from nowhere.
- CV source file in the vault includes a personal phone number — must not be
  copied to any public page (see `AGENTS.md` §1).

## Steps

- [ ] **Step 1 — Rewrite `about.markdown`.** Pull positioning from
      `joko_pawitro_HVC.md`'s PROFESSIONAL SUMMARY, rewritten for a personal-site
      voice (not CV-bullet voice): HV cable + offshore wind digitalization
      specialist, ~15 years spanning mechanical/asset-integrity → electrical/data
      science, currently pursuing MSc (Sustainable Electrical Engineering, ITS,
      thesis on dynamic line rating). Do not include phone number. Confirm
      wording with Joko before treating as final (this is public-facing identity
      copy, not boilerplate).
- [ ] **Step 2 — Rewrite `index.markdown` tagline.** Replace the generic
      "mechanical-electrical engineering analysis, data science, multiphysics
      simulation and business analytics" line with something that reflects the
      current specialization + thesis-in-progress, kept short (this is the
      hero subtitle, not a bio).
- [ ] **Step 3 — Update `_config.yml` → `occupations`.** Correct the Ørsted
      entry's role/date to match current title (Cable Specialist, Export Cable
      Systems, May 2025–present); decide with Joko whether to show one Ørsted
      entry or split by role-progression (Cable Monitoring Specialist →
      Electrical Cable Specialist → current); add an Elnusa entry (2011–2018)
      for the asset-integrity throughline. Decide whether Practicum stays (it's
      a teaching/mentoring credential, not core to the cable-engineering
      narrative) and whether the CTO/consulting stint (2018–2022) is worth a
      line — **flag both as human decision points, not something to decide
      unilaterally** (see below).
- [ ] **Step 4 — Wire up `_includes/navbar.html`.** Uncomment and rebuild the
      nav menu with real, working links: About (`/#aboutme`), Thesis Progress
      (`/thesis/progress/...`), and Contact (email or LinkedIn — decide which).
      Drop the placeholder "2-Dimensional" link entirely; decide with Joko
      whether `quiz/cohort_04_ind.html` (Practicum-cohort-specific) belongs in
      public nav at all or should stay unlinked/removed.
- [ ] **Step 5 — Resolve `_includes/highlights.html`.** Either replace the
      four Lorem Ipsum blocks with real content (e.g. cable monitoring / DLR /
      risk-based design / data science as four pillars) and re-enable it in
      `_layouts/home.html`, or delete the include and its Chart.js dependency
      entirely if not worth writing real copy for right now.
- [ ] **Step 6 — Housekeeping.** Remove the unused `jekyll-theme-hydejack`
      dependency from `Gemfile.lock` (theme is commented out in `_config.yml`
      and not in use); run `bundle install` locally to confirm the lockfile
      still resolves cleanly after removal.
- [ ] **Step 7 — Privacy pass.** Before committing, grep the diff for the
      phone number and any other CV-only detail (references, salary-adjacent
      figures) that shouldn't be public; confirm only email/LinkedIn/GitHub
      appear.

## Out of scope

- A full visual/design refresh (new color scheme, typography, hero layout
  redesign) — this plan is content + information-architecture only. If wanted,
  it should be its own follow-up `rpi/` plan once the content itself is
  correct, so design changes aren't reviewed at the same time as fact changes.
- Migrating off Jekyll/Bulma/GitHub Pages — assessed and rejected in
  `AGENTS.md` §4; not revisited here.
- Turning `_posts/` into an active blog (thesis write-ups, platform-vision
  notes) — worth considering later, but it's a content-strategy decision, not
  a refresh of what's already stale.

## Human decision points

- Should the Ørsted `occupations` entry show only the current role, or all
  three internal role transitions (Cable Monitoring Specialist → Electrical
  Cable Specialist → Cable Specialist, Export Cable Systems)? Showing the
  progression tells a better story but adds visual bulk to a card-based layout
  built for one entry per company.
- Does Practicum (mentoring) still belong on the public site, given it predates
  the current HV cable specialization and isn't mentioned as a highlight in
  the current CV's own framing?
- Is the CTO/consulting stretch (PT Intelegensi Artifisial Indonesia / PT
  Lentera Data Analitika, 2018–2022) worth surfacing publicly, given it also
  ties into the long-term engineering-platform business vision — or does that
  belong in a future dedicated section instead of the occupations list?
- Does `quiz/cohort_04_ind.html` get linked, left orphaned as-is, or removed?
  It's cohort-specific Practicum material, not general-audience content.
- Contact channel for the nav: email vs. LinkedIn vs. both?
