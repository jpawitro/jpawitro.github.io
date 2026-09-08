# Plan: Content, occupations, and navigation refresh

**Date:** 2026-09-09
**Status:** Not started

## Objective

Bring the site's content back in line with Joko's actual current profile
(HV Cable Specialist at Ørsted, MSc candidate, ~15 years engineering
background) and make the thesis progress work reachable from the site,
without touching the underlying stack (Jekyll + Bulma + GitHub Pages stays
as-is — see `AGENTS.md` §4).

## Research (recon already done — 2026-09-09)

- `about.markdown` is unedited Jekyll/Minima boilerplate — never customized.
- `index.markdown` tagline is generic and doesn't mention the current
  specialization, thesis, or platform-building angle.
- `_config.yml` → `occupations` currently lists Ørsted (titled "Cable
  Monitoring Specialist" — that was the Feb'23–Jan'24 role; current per
  `despicable-mind/05-professional/cv/joko_pawitro_HVC.md` is "Cable
  Specialist, Export Cable Systems," May 2025–present) and Practicum, with a
  single generic `responsibility` paragraph — no room for scope, projects,
  capabilities, or stack.
- `_includes/highlights.html` is Lorem Ipsum, currently commented out in
  `_layouts/home.html`.
- `_includes/hero.html` renders a personal social-icon row: github, twitter,
  linkedin, instagram, youtube — sourced from `_config.yml` → `social`.
- `_includes/navbar.html` has all nav links commented out — no working
  navigation exists. Brand mark is hardcoded plain text: "JPAWiTRO" +
  ".space" (same ".space" also appears in `_config.yml` → `title`: "Jpawitro's
  Space").
- `thesis/progress/` contains dated report files (currently one:
  `2026-09-07_data-cuaca-power-curve-model-wind-to-load.html`) plus
  `favicon.png` and `styles.css` — no index page exists, and nothing links
  to the folder.
- `quiz/cohort_04_ind.html` exists — Practicum-cohort-specific material, to be
  removed.
- CV source file in the vault includes a personal phone number — must not be
  copied to any public page (see `AGENTS.md` §1).

## Decisions (resolved 2026-09-09)

- **Occupations: current role only, no progression, no other companies.**
  Drop Practicum entirely. Don't add Elnusa either — the `occupations` section
  is scoped to the current job, not a career-history section.
- **Ørsted card gets richer content**, not just a one-line `responsibility`:
  scope of work, projects tied to the current role (TEEM, RBCD, DTS/DAS
  exposure monitoring, DLR), highlighted capabilities, and main stack
  (Python, IEC 60287 / CIGRE TB 880 & TB 908, DNV standards, etc.). Needs a
  small schema extension in `_config.yml` + `_includes/occupations.html`
  (structured fields, not one paragraph).
- **`highlights.html` is superseded, not revived.** Its intended job
  (capability highlights) now lives inside the enriched Ørsted card. Remove
  the include and its Chart.js dependency rather than filling in the Lorem
  Ipsum.
- **`quiz/` folder is removed** — Practicum-cohort-specific, not relevant to
  the current site direction.
- **Personal social icons trimmed to GitHub + LinkedIn only.** Twitter,
  Instagram, and YouTube icons come out of `hero.html`. (This is about the
  personal social row — the per-company social links inside `occupations.html`
  are Ørsted's own channels and are a separate, unaffected thing.)
- **Contact nav item points to LinkedIn.** Given only GitHub and LinkedIn
  remain as personal channels, and GitHub is already the repo's own home,
  LinkedIn is the more natural "get in touch professionally" link.
- **Logo left alone for this pass.** No brand/wordmark restyle in this plan —
  see Out of scope.
- **Thesis progress index — layout direction (design below), resolved:**
  Reverse-chronological list, most recent first, one row per report, each
  showing a formatted date and a title derived from the filename — no manual
  per-entry maintenance beyond dropping a new dated file into the folder.
  - **Filename convention assumed:** `YYYY-MM-DD_kebab-case-title.html`
    (matches the existing file). Parsing rule: first 10 characters = date;
    everything after the following `_` and before `.html` = the slug;
    render the date as e.g. "07 Sep 2026"; render the title by replacing
    dashes with spaces and capitalizing each word (e.g.
    `data-cuaca-power-curve-model-wind-to-load` → "Data Cuaca Power Curve
    Model Wind To Load").
  - **Source list:** iterate the `.html` files directly under
    `thesis/progress/` (via `site.static_files`, filtered to that path and to
    `.html`), excluding `index.html` itself. `favicon.png` / `styles.css` are
    assets, not entries — exclude anything that isn't `.html`.
  - **Visual style:** a simple Bulma `list` (or single-column stacked cards,
    consistent with the `occupations` card style) — date as a small muted
    label, title as the clickable link. No pagination needed at this volume;
    revisit only if the report count grows large.

## Steps

- [ ] **Step 1 — Rewrite `about.markdown`.** Pull positioning from
      `joko_pawitro_HVC.md`'s PROFESSIONAL SUMMARY, rewritten for a personal-site
      voice (not CV-bullet voice): HV cable + offshore wind digitalization
      specialist, ~15 years spanning mechanical/asset-integrity → electrical/data
      science, currently pursuing MSc (Sustainable Electrical Engineering, ITS,
      thesis on dynamic line rating). No phone number. Confirm wording with
      Joko before treating as final — this is public-facing identity copy.
- [ ] **Step 2 — Rewrite `index.markdown` tagline.** Replace the generic
      "mechanical-electrical engineering analysis, data science, multiphysics
      simulation and business analytics" line with something reflecting the
      current specialization + thesis-in-progress. Keep it short (hero
      subtitle, not a bio).
- [ ] **Step 3 — Extend the `occupations` schema and rewrite the Ørsted
      entry.** In `_config.yml`, replace the single `responsibility` string
      with structured fields, e.g. `scope`, `projects` (list), `capabilities`
      (list), `stack` (list) — content sourced from `joko_pawitro_HVC.md`'s
      "Cable Specialist, Export Cable Systems" entry and CORE COMPETENCIES /
      SOFTWARE PROFICIENCY sections. Update `_includes/occupations.html` to
      render the new fields (scope paragraph + a few short lists) instead of
      the current single paragraph. Remove the Practicum entry entirely.
- [ ] **Step 4 — Remove `_includes/highlights.html`** and its
      `<script src=".../chart.js">` include, and delete the commented-out
      `{% include highlights.html %}` line in `_layouts/home.html`.
- [ ] **Step 5 — Build the thesis progress index.** Add
      `thesis/progress/index.html` implementing the filename-parsing +
      reverse-chronological list design specified above.
- [ ] **Step 6 — Trim `_includes/hero.html` social icons** to GitHub and
      LinkedIn only; remove the Twitter, Instagram, and YouTube `<a>` blocks
      (and, for cleanliness, their now-unused keys under `_config.yml` →
      `social` — optional, but avoids dead config).
- [ ] **Step 7 — Wire up `_includes/navbar.html`.** Uncomment and rebuild the
      nav menu with: About (`/#aboutme`), Thesis (`/thesis/progress/`), and
      Contact (LinkedIn profile URL). Drop the placeholder "Projects" / "Blog"
      / "2-Dimensional" links entirely — no content backs them right now.
- [ ] ⚠️ **Step 8 — Remove the `quiz/` folder** (`quiz/cohort_04_ind.html`).
      Deletion, recoverable via git history, but flagging per convention
      since it's a folder removal rather than an edit.
- [ ] **Step 9 — Housekeeping.** Remove the unused `jekyll-theme-hydejack`
      dependency from `Gemfile.lock` (theme is commented out in `_config.yml`
      and not in use); run `bundle install` locally to confirm the lockfile
      still resolves cleanly.
- [ ] **Step 10 — Privacy pass.** Before committing, check the diff for the
      phone number or any other CV-only detail that shouldn't be public;
      confirm only email/LinkedIn/GitHub appear anywhere on the site.

## Out of scope

- **Logo/brand restyle** — left alone in this pass, per decision above.
- **Removing ".space"** (`_includes/navbar.html` and `_config.yml` → `title`)
  — deferred to a later, separate plan, to be done alongside (or after) the
  logo work once Joko has settled on the replacement naming/domain.
- A full visual/design refresh beyond what's implied by Steps 3–6 (new color
  scheme, typography, hero layout redesign) — its own follow-up `rpi/` plan
  if wanted, once content is correct.
- Migrating off Jekyll/Bulma/GitHub Pages — assessed and rejected in
  `AGENTS.md` §4.
- Turning `_posts/` into an active blog (thesis write-ups, platform-vision
  notes) — a content-strategy decision, not part of this refresh.

## Human decision points

None outstanding — all prior open questions (occupations scope, contact
channel, thesis index format, logo) are resolved above. Implementer should
still surface anything unexpected found mid-execution rather than improvising
past it (see `AGENTS.md` §2).
