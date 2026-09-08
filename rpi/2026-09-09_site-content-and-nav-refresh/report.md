# Report: Content, occupations, and navigation refresh

**Date:** 2026-09-09
**Status:** Implemented, pending human review before push (see gate below).

## Summary

All 10 plan steps executed. Site was built locally with Jekyll 4.3.4 (isolated
gem path, not the system Ruby install) to confirm every template change
renders without Liquid errors, and the rendered output was checked for the
phone number and other CV-only detail. Nothing pushed — this stays local
pending Joko's review, per `AGENTS.md` §2's human-in-the-loop gate.

## Step-by-step

- [x] **Step 1 — Rewrite `about.markdown`.** Done. New copy: HV cable +
      offshore wind digitalization specialist framing, the ~15-year
      mechanical→electrical/data arc, current MSc + DLR thesis, links to
      LinkedIn/GitHub/thesis page. No phone number. **This is a wording draft
      — flagged in the plan as needing Joko's confirmation before treating as
      final; review [about.markdown](about.markdown) specifically.**
- [x] **Step 2 — Rewrite `index.markdown` tagline.** Done — replaced the
      generic multiphysics/business-analytics line with a short line naming
      HV cable engineering, offshore wind digitalization, and the DLR thesis.
- [x] **Step 3 — Extend `occupations` schema, rewrite Ørsted entry.** Done.
      `_config.yml` now has `scope`, `projects` (list), `capabilities` (list),
      `stack` (list) replacing the single `responsibility` string; role
      updated to "Cable Specialist, Export Cable Systems" (May 2025–present).
      Content sourced from `joko_pawitro_HVC.md`'s matching experience entry
      and CORE COMPETENCIES / SOFTWARE PROFICIENCY sections.
      `_includes/occupations.html` updated to render scope + three short
      lists instead of one paragraph. Practicum entry removed entirely.
- [x] **Step 4 — Remove `_includes/highlights.html`.** Done — file deleted,
      Chart.js dependency went with it, and the commented-out include line
      in `_layouts/home.html` is gone.
- [x] **Step 5 — Build thesis progress index.** Done —
      [thesis/progress/index.html](thesis/progress/index.html) added.
      Iterates `site.static_files` under `/thesis/progress/`, filters to
      `.html` excluding `index.html`, sorts reverse-chronological by
      filename, and parses date/title per the plan's convention. Verified
      against the one existing report: renders "Data Cuaca Power Curve Model
      Wind To Load" / "07 Sep 2026", linking to the file.
      **One implementation snag worth flagging:** the first version used
      `{% unless forloop.last %} {% endunless %}` to insert a space between
      words — Liquid treats a block whose entire body is whitespace as
      "blank" and silently drops it, which produced "DataCuacaPowerCurve…"
      with no spaces. Fixed by accumulating the title into a string with
      `assign`/`append` instead of relying on a whitespace-only tag body.
      Caught by an actual `jekyll build`, not just a read-through.
- [x] **Step 6 — Trim `hero.html` social icons.** Done — Twitter, Instagram,
      YouTube `<a>` blocks removed, GitHub + LinkedIn remain.
      `_config.yml` → `social` also had the now-unused `twitter` and
      `instagram` keys removed (the plan's "optional" cleanup); left
      `medium:` alone since it was already unused before this plan and isn't
      one of the icons this step is about.
- [x] **Step 7 — Wire up `navbar.html`.** Done — uncommented and rebuilt with
      About (`/#aboutme`), Thesis (`/thesis/progress/`), Contact (LinkedIn,
      `http://linkedin.com/in/{{ site.social.linkedin }}`, opens in a new
      tab). Placeholder Projects/Blog/2-Dimensional links and the old
      Telegram bot Contact link are gone.
- [x] ⚠️ **Step 8 — Remove `quiz/` folder.** Done via `git rm -r quiz` —
      `quiz/cohort_04_ind.html` staged for deletion, recoverable from git
      history.
- [x] **Step 9 — Housekeeping (Gemfile.lock).** Done, with a deviation from
      the literal instruction worth flagging: a plain `bundle install`/
      `bundle lock` on this machine re-resolves the *whole* graph (this repo
      had never been locked for Bundler 2.3.26 + a modern Ruby before), which
      would have bumped ~8 transitive gems for reasons unrelated to this
      task. Instead I hand-removed only the `jekyll-theme-hydejack` and
      `jekyll-include-cache` (hydejack's own sub-dependency, unused by
      anything else) entries from the lockfile, then verified the result for
      real: `bundle lock --add-platform arm64-darwin-25` (needed so the
      lockfile can install on Joko's Mac at all — it was previously
      `x86_64-linux`-only, presumably GitHub Pages' CI platform) followed by
      a full `bundle install` into an isolated temp path. Installed cleanly:
      32 gems, no hydejack. Net lockfile diff: hydejack + jekyll-include-cache
      removed, `arm64-darwin-25` added to `PLATFORMS` (`x86_64-linux` kept),
      no other gem versions changed. Ruby/Bundler used: system Ruby 2.6.10
      with Bundler 2.3.26 installed to the user gem dir (`gem install
      bundler:2.3.26 --user-install`) since the pinned Bundler version
      wasn't present system-wide — that install is local to this machine's
      user gem path, not part of the repo.
- [x] **Step 10 — Privacy pass.** Done. Diffed and grepped the full local
      Jekyll build output for the phone number (`5936`, `+60 17`) and found
      one incidental substring match — inside base64-encoded font data in
      the pre-existing (untouched) thesis report HTML, not the actual number.
      Confirmed only email, LinkedIn, and GitHub appear anywhere in the
      changed content.

## Verification performed

- `bundle install` into an isolated path (`/tmp/...`, not committed) to
  confirm the trimmed `Gemfile.lock` resolves and installs with no
  `jekyll-theme-hydejack`.
- `jekyll build` of the full site using that isolated gem set — completed
  with no Liquid/build errors.
- Read the generated HTML for: homepage occupations card (single Ørsted
  entry, new structured fields, Practicum gone), navbar (About/Thesis/Contact
  links resolve to the intended URLs), hero social icons (GitHub + LinkedIn
  only), thesis progress index (correct title/date formatting).
- Grepped the build output for the phone number and for stray
  `highlights.html`/Chart.js/Practicum/quiz references — none found outside
  the one coincidental base64 substring noted above.
- All temporary verification artifacts (`/tmp` bundle path and build output,
  a stray local `.bundle/config` created by the verification `bundle
  install`) were removed; they are not part of the working tree.

## Deviations from the plan

1. **Step 9** used a hand-edited, verified lockfile instead of a raw `bundle
   install`/`bundle lock` run, to avoid an unrelated ~8-gem version bump —
   see Step 9 note above for the reasoning and what was actually verified.
2. **Step 5** needed a small Liquid workaround not anticipated in the plan
   (the whitespace-blank-block issue) — noted above for anyone touching this
   template later.

Neither deviation changes the plan's intent; both are noted per `AGENTS.md`
§2 ("stop and note it in the report rather than improvising past it").

## Outstanding / not part of this plan

- `assets/images/Practicum.png`, `PracticumLogo_SVG.svg`, and
  `practicum_banner.png` are now unreferenced (Practicum entry removed from
  `_config.yml`). The plan didn't call for deleting them and I left them
  alone — flagging in case Joko wants a follow-up cleanup.
- `about.markdown` wording (Step 1) is a first draft of public-facing
  identity copy and should be read closely before this is pushed, per the
  plan's own instruction to confirm wording first.

## Human decision / confirmation needed before push

Per `AGENTS.md` §2, this stays local. Before pushing, please:
1. Read and confirm/adjust the [about.markdown](about.markdown) wording.
2. Skim the new Ørsted occupations card content in `_config.yml` /
   [_includes/occupations.html](_includes/occupations.html) for accuracy.
3. Say the word to push (or ask for a branch instead of pushing to `main`
   directly, since current branch is `main`).
