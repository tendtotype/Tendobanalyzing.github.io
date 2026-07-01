# CLAUDE.md

Guidance for AI assistants working in this repository.

## What this is

A **static personal portfolio website** for Tendo Bosa, a data analyst. It is
served via **GitHub Pages** from `tendtotype/Tendobanalyzing.github.io`, so the
site is published directly from the files in the repository root — there is no
build step, no server, and no package manager. Whatever is committed to the
default branch is what goes live.

The design is the free **"Massively" template by HTML5 UP** (html5up.net,
CCA 3.0 license). The portfolio content is a set of cards linking out to Tableau
Public dashboards and a Kaggle notebook.

## Layout

```
index.html            The live homepage — portfolio landing page (edit this for content)
generic.html          Template's generic single-column page (unused, kept as reference)
elements.html         Template's component/style reference page (unused, kept as reference)
assets/
  css/main.css        COMPILED stylesheet actually loaded by the pages
  css/noscript.css    Fallback styles when JS is disabled
  css/fontawesome-all.min.css
  sass/               SCSS SOURCE for main.css / noscript.css (see "Styling" below)
  js/main.js          Site behavior (parallax intro, nav panel, scroll effects)
  js/*.min.js         Vendored libs: jQuery, Scrollex, Scrolly, browser.js, breakpoints.js
  webfonts/           Font Awesome icon fonts
images/               Images referenced by index.html (e.g. images/C02emissions.jpeg)
*.jpg / *.jpeg / *.webp / *.png  Duplicate/loose image copies in the repo root
html5up-massively/    Pristine, untouched copy of the original template (reference only — do NOT edit)
README.txt            Original template readme
LICENSE.txt / (html5up-massively/LICENSE.txt)  Template license
```

## Key conventions

- **`index.html` is the site.** Almost all content edits happen here. It holds
  the intro, nav, the featured project, the `<section class="posts">` project
  cards, and the contact footer. Each project card is an `<article>` with a
  title, an image link, a description, and a "View Project" button pointing to
  an external Tableau/Kaggle URL.
- **Images live in `images/`.** Cards reference paths like
  `images/amsterdamairbnb.jpeg`. Note that copies of many images also sit in the
  repo root and in `html5up-massively/images/` — the *root-level `images/`*
  folder is the one the live page uses. When adding a project, drop the image in
  `images/` and reference it from there.
- **Do not edit `html5up-massively/`.** It is a clean copy of the vendor
  template kept for reference. Real changes go in the repo root and `assets/`.
- **`generic.html` and `elements.html`** are template leftovers not linked from
  the live nav. Leave them unless explicitly asked to build them out.

## Styling (SASS → CSS)

`assets/css/main.css` is **compiled output**, not hand-authored, and it is the
file the browser loads. Its source is `assets/sass/main.scss`, which imports
partials under `assets/sass/base/`, `components/`, `layout/`, and `libs/`.

There is **no build tooling checked in** (no `package.json`, Gruntfile, or
gulpfile). So there are two ways to change styles:

1. **Small/quick tweaks:** edit `assets/css/main.css` directly. Simplest, and it
   takes effect immediately on GitHub Pages. Downside: the SCSS source drifts
   out of sync.
2. **Proper changes:** edit the `.scss` partials, then recompile, e.g.
   `sass assets/sass/main.scss assets/css/main.css` (and likewise for
   `noscript.scss`). Commit both the changed SCSS and the regenerated CSS.

Prefer option 2 when possible and keep SCSS and CSS in sync. If you only touch
the CSS, say so in the commit message so the SCSS drift is visible.

## Local preview

No server required — open `index.html` in a browser, or run a static server from
the repo root for correct relative paths:

```
python3 -m http.server 8000    # then visit http://localhost:8000
```

## Deployment

GitHub Pages serves the repository automatically. There is no CI/CD, no build,
and no `.nojekyll` file. Merging to the default branch (`main`) publishes the
site. Verify visual changes by previewing locally before committing.

## Git workflow

- The default/production branch is `main`.
- Do feature work on a dedicated branch, commit with clear messages, and push
  with `git push -u origin <branch-name>`.
- Only merge to `main` when the change is ready to go live, since `main` is the
  published site.

## Common tasks

- **Add a portfolio project:** add the image to `images/`, then copy an existing
  `<article>` block inside `<section class="posts">` in `index.html` and update
  its title, description, image `src`, and the two external project URLs.
- **Change the featured project:** edit the `<article class="post featured">`
  block near the top of `#main` in `index.html`.
- **Update contact / social links:** edit the intro paragraph, the `<nav>`
  `ul.icons`, and the contact `<footer>` in `index.html` (LinkedIn, Kaggle,
  email are all repeated in a couple of spots — update each).
- **Restyle:** follow the "Styling" section above.
