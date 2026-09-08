# AI Instructions — jpawitro.github.io

This file is the entry point for any AI assistant (Claude Code, Codex, Gemini, etc.)
working in this repository. Read it before making any structural change —
rewriting layouts/includes, editing `_config.yml`, or touching content that
describes Joko's career, education, or credentials.

## 1. Source of truth

- **Biographical / career / credential facts** (job titles, dates, employers,
  education, certifications, thesis status) live in the Obsidian vault, not in
  this repo:
  - `despicable-mind/05-professional/cv/joko_pawitro_HVC.md` — most current
    general-purpose CV; treat as primary source for the site's About/Occupations
    content unless told otherwise.
  - `despicable-mind/05-professional/00-professional-moc.md` — index of all
    CV/cover-letter variants, in case a different targeted framing is asked for.
  - `despicable-mind/05-professional/career-development/` — roadmap, Saudi
    transition plan, and other narrative context that may inform tone/framing.
  - `despicable-mind/03-stem/` and `despicable-mind/04-business-investing/` —
    thesis research and the engineering-platform business vision, if either is
    ever summarized on the site.
  This repo does not keep a synced copy of any of this. **Never invent or
  extrapolate a job title, date, metric, or credential that isn't in the vault
  source.** If a fact needed for a content update isn't in the vault, stop and
  ask rather than guessing or copying stale content already on the site.
- **Site code, layout, templates, and assets** (`_layouts/`, `_includes/`,
  `assets/`, `_config.yml` structure, `_posts/`, `thesis/`, `quiz/`) — this repo
  is the source of truth. The vault has no opinion on Jekyll/Bulma/JS
  implementation details.
- **Privacy check on every content pull from the vault:** CV files in the vault
  include a personal phone number. This is a **public** GitHub Pages site —
  never publish the phone number. Email (`jpawitro@protonmail.com`), LinkedIn,
  and GitHub handles are fine; phone number is not, regardless of what the CV
  source file contains.

## 2. RPI workflow — mandatory for any multi-step or repo-altering task

Before executing a task that changes more than a single file, or that touches
`_config.yml`, git history, or repository structure:

1. **Research/Recon** — read what's actually on the site and in the relevant
   vault source before proposing changes.
2. **Plan** — write a dated plan file at `rpi/<YYYY-MM-DD>_<short-slug>/plan.md`
   (see `rpi/README.md` for the template). The plan is a checklist. Do not
   start executing until the plan file exists on disk.
3. **Implement** — execute the plan step by step. Do not silently skip or
   reinterpret a step; if a step turns out to be wrong or unsafe, stop and note
   it in the report rather than improvising.
4. **Report** — write `rpi/<YYYY-MM-DD>_<short-slug>/report.md` in the same
   folder, dated, marking each plan item **Done / Failed / Skipped**, with a
   one-line reason for anything not Done.

**Human-in-the-loop gate:** after writing the report, stop. Do not `git push`
or publish to the live site without Joko explicitly confirming after reading
the report. This is a public-facing personal site, so treat any change to
`about.markdown`, `index.markdown`, or the `occupations` list in `_config.yml`
as review-required, not autopilot-safe — it's Joko's professional identity,
not boilerplate copy.

## 3. Repository layout

| Path | Holds |
|---|---|
| `_config.yml` | Site-wide data: title, `occupations` list, `social` handles |
| `_layouts/` | Page skeletons (`default`, `home`, `page`, `post`, `comingsoon`) |
| `_includes/` | Reusable blocks (`hero`, `about`, `occupations`, `navbar`, `footer`, `head`, `highlights`) |
| `_posts/` | Blog posts (currently just the default Jekyll welcome post — unused) |
| `assets/css`, `assets/js` | Custom CSS on top of Bulma (CDN); vanilla JS for navbar burger toggle |
| `thesis/progress/` | Standalone hand-built HTML/CSS thesis progress write-ups — not wired into Jekyll templating, not linked from nav |
| `quiz/` | Standalone HTML quiz page — not linked from nav |

`about.markdown` and `index.markdown` are page content (Liquid front matter +
Markdown), not includes — they're the files that currently still carry
unedited Jekyll/Minima boilerplate text and need real content.

## 4. General rules

- Prefer minimal, targeted diffs. Don't touch files outside the task's scope.
- Keep the stack as-is (Jekyll + Bulma via CDN, deployed on GitHub Pages).
  Don't introduce a build step, a different SSG, or a new CSS framework
  without being explicitly asked — this has already been assessed as the
  right fit for a low-content personal/portfolio site.
- Don't resurrect the `highlights.html` Lorem Ipsum block as-is; it's
  currently commented out in `_layouts/home.html` for a reason. Either
  replace it with real content or leave it out.
- Don't add tracking/analytics scripts, third-party embeds, or new social
  platforms without being asked.
