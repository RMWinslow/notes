---
nav_exclude: True
search_exclude: True
---

# Claude Notes — notes repo

This file serves as Claude's working memory for the `notes` repo
(deployed at `www.rmwinslow.com/notes/`).

## Writing Conventions

Do not drop articles ("a", "an", "the") from commit messages, prose, or any
other written text. Write in complete, natural English.

Commit messages should explain reasoning and motivation ("why"), not restate
the diff ("what").

When migrating or reorganizing files, separate the mechanical move from any
edits to the moved files. First commit the files with their original content
preserved exactly, then commit modifications as a separate change.

## Project Context

This is the economics notes subsite of Robert Winslow's personal academic
website. It uses the `RMWinslow/JTD-RMW` theme (a fork of Just the Docs),
with `baseurl: /notes` so that all pages are served under
`www.rmwinslow.com/notes/`.

The main site repo is `RMWinslow.github.io` (deployed at
`www.rmwinslow.com`). There are several sibling repos sharing the same theme:
`posts` (blog), `bib` (bibliography), `games` (game rules), and `circe`
(literary text). All are served as subdirectories of `www.rmwinslow.com`.

### What lives here

- **`302/`** — Intermediate Macro (Econ 3102) notes. These are Jekyll markdown
  pages with frontmatter, organized under a nav hierarchy rooted at
  `topic-overview.md`. They include interactive kgjs graphs (`302/graphs/`),
  Highcharts graphs (`302/highcharts/`), images, and supporting assets. This
  was the first content migrated from the main repo (2026-03-19), and the
  directory was renamed from `3102/` to `302/` on 2026-03-20.

- **`202/`** — Principles of Macro. Currently contains only
  `inflation-costs.md` (migrated 2026-03-20).

- **`econ/`** — Legacy economics content migrated from the main repo on
  2026-03-20. These are pre-Jekyll HTML files without frontmatter — they don't
  participate in the nav tree or search index, but they're actively served as
  static pages. The directory contains:
  - `econ/teaching/` — Interactive graphs, equilibrium walkthroughs,
    intertemporal consumer problems, typesetting guides, and problem sets
    with SVG figures, all for Econ 3102.
  - `econ/macroprelim/` — Macro prelim study notes (Chari, Jones, Kehoe
    sections), organized by professor.
  - `econ/tradeprelim/` — Trade prelim study notes (Amador, Fitzgerald, Kehoe
    sections), with LyX source files alongside the HTML.
  - `econ/presentations/` — Percolation/graph theory slides (Reveal.js) and
    a presentation list.
  - `econ/nonsense/mathsymbols.html` — A math symbols reference page.
  - `econ/UMNelectives.md` — A Jekyll page listing UMN econ electives
    (`nav_exclude: true`). Robert is no longer at UMN.

- **`_detritus/`** — Unsorted research files from the `papersdrafts` repo
  migration. Not part of the notes content.

### CSS references in legacy HTML

The HTML files under `econ/` use root-relative CSS paths like
`/assets/css/sakura.css`. These resolve correctly because all repos are served
under the same domain (`www.rmwinslow.com`), and the CSS files live in the
main repo's `assets/css/` directory. The CSS is not duplicated here. If the
main repo ever moves or renames those files, the paths here will break.

The color-variant stylesheets (`sakuraGreen.css`, `sakuraPink.css`,
`sakuraBlue.css`) are professor-specific theming for the macro prelim notes
(Chari → green, Kehoe → pink, Jones → blue).

### Interactive graphs

There are two generations of interactive economics graphs, both nav-hidden but
actively served:

- **`302/graphs.md`** uses kgjs (KineticGraphs). It loads YML config files
  from `302/graphs/*.yml` and renders them client-side with `kg3d.0.2.6.js`.
  These support click-and-drag interaction.

- **`302/graphs2.md`** uses Highcharts. It embeds the 9 HTML files in
  `302/highcharts/` via iframes and provides standalone links to each. These
  are self-contained and intentionally kept as a working fallback.

**Known issue:** Some pages load kgjs, which bundles its own KaTeX. When the
theme also loads KaTeX (or MathJax, as configured here), the page can stutter.
The `302/graphs.md` page should be checked for conflicts with `math: mathjax`
set in `_config.yml`.

## How Redirects Work

When content moved from the main repo to this repo, redirect stubs were placed
in the main repo's `redirects/` directory. Each stub is a minimal markdown file
with only frontmatter:

```yaml
---
permalink: /old/path
redirect_to: /notes/new/path
---
```

Jekyll + `jekyll-redirect-from` generates a lightweight HTML page at the old
URL containing a JavaScript redirect, an instant `<meta refresh>`, a
`<link rel="canonical">`, and `<meta name="robots" content="noindex">`. Google
treats instant meta refresh as a permanent redirect.

The redirects are single-hop — no chains. A visitor hitting the old URL goes
straight to the new one.

### Redirect inventory

There are currently 91 redirect stubs in the main repo covering content that
moved here:

- **26 stubs** for the `302/` notes migration (2026-03-19) — covers all 21
  content pages, 1 parent page, 3 nav-hidden pages, and 2 legacy
  twoperiod-consumer aliases. These redirect from `/3102/...` to
  `/notes/302/...`.

- **65 stubs** for the `econ/` migration (2026-03-20) — covers 1 MD file
  (UMNelectives) and 64 HTML files. These redirect from `/econ/...` to
  `/notes/econ/...`.

The 302/ pages also have `redirect_from` entries in their own frontmatter
covering the intermediate `/notes/3102/...` URLs (from the brief period when
the directory was still named `3102/` in this repo).

### If you rename or move a page in this repo

1. Update the redirect stub in the main repo's `redirects/` directory to point
   to the new URL.
2. If the page had a `redirect_from` in its own frontmatter, update or remove
   that too.
3. Update the entry in the main repo's `redirects/INDEX.md`.
4. Verify there are no redirect chains (old URL → intermediate URL → final
   URL). Every redirect should be a single hop.

The full redirect maintenance procedure is documented in the main repo's
`redirects/INDEX.md`, including a curl-based validation checklist.

## Known Broken Links (from the main repo audit, 2026-03-16)

These broken links were identified before the files moved here. The paths are
now relative to this repo's `econ/` directory. The CSS issues were partially
fixed (all `sakura.css` references were updated to root-relative paths on
2026-03-20), but the cross-file reference issues remain.

### Cross-file reference issues in `econ/macroprelim/`

| Source file | Link target | Issue |
|---|---|---|
| `econ/macroprelim/Jones/HumanCapital.html` | `../FlowChartKey.html` | Not found; file is in `Concepts/flowchartkey/` |
| `econ/macroprelim/Jones/HumanCapital.html` | `KehoeSearchLabels.png` | Not found in `Jones/`; file is in `Kehoe/` |
| `econ/macroprelim/Jones/HumanCapital.html` | `crossingProof.html` | Not found in `Jones/`; file is in `Kehoe/` |
| `econ/macroprelim/Jones/dynamicprogramming.html` | `../FlowChartKey.html` | Same FlowChartKey issue |
| `econ/macroprelim/Jones/dynamicprogramming.html` | `KehoeSearchLabels.png` | Same missing image |
| `econ/macroprelim/Jones/dynamicprogramming.html` | `crossingProof.html` | Same missing file |
| `econ/macroprelim/Kehoe/Search.html` | `../FlowChartKey.html` | Same FlowChartKey issue |
| `econ/macroprelim/Kehoe/dp.html` | `../FlowChartKey.html` | Same |

These are relative-path links that assume a different directory layout than
what actually exists. The FlowChartKey links should point to
`../Concepts/flowchartkey/FlowChartKey.html`, and the Kehoe-specific files
should use `../Kehoe/` paths.

### Malformed references in `econ/teaching/3102psets/`

| Source file | Link target | Issue |
|---|---|---|
| `econ/teaching/3102psets/HW1_dataGraphs.html` | `HW1_GrowthGraphs/https://code.highcharts.com/highcharts.js` | Local path prefix before an external URL |
| `econ/teaching/3102psets/HW2_dataGraphs.html` | `HW2_BCycleGraphs/https://code.highcharts.com/highcharts.js` | Same malformed pattern |

### Broken Reveal.js references in `econ/presentations/`

| Source file | Link target | Issue |
|---|---|---|
| `econ/presentations/percolationSlides.html` | `../../styles/reveal/css/reveal.css` | No `reveal/` directory has ever existed |
| `econ/presentations/percolationSlides.html` | `../../styles/reveal/css/theme/white.css` | Same |
| `econ/presentations/percolationSlides.html` | `../../styles/reveal/js/reveal.js` | Same |

The Reveal.js slides have never had working local CSS/JS references. They may
have relied on a CDN fallback or simply been broken since creation.

### Broken image in `302/measurement-gdp.md`

The page contains `IMAGEURLHERE` as a placeholder for a broken image reference.

## TODOs

- [ ] Fix the cross-file reference issues in `econ/macroprelim/` listed above.
  The Jones pages link to Kehoe files and FlowChartKey using wrong relative
  paths. These have been broken since the files were originally written.
- [ ] Fix the malformed Highcharts URLs in `econ/teaching/3102psets/`. The
  `<script>` tags prepend a local directory path to the external CDN URL.
- [ ] Decide what to do about the Reveal.js slides
  (`econ/presentations/percolationSlides.html`). The Reveal.js CSS/JS
  references have always been broken. Options: add a local copy of Reveal.js,
  switch to CDN references, or accept them as non-functional.
- [ ] Fix the `IMAGEURLHERE` placeholder in `302/measurement-gdp.md`.
- [ ] Check whether `math: mathjax` in `_config.yml` conflicts with the kgjs
  pages that load their own KaTeX.
- [ ] Consider adding `search_exclude: true` to legacy HTML files in `econ/`
  that lack frontmatter, to keep them out of the search index. There are
  roughly 65 such files.
- [ ] Add a `nav_external_links` entry in `_config.yml` pointing back to the
  main site (`www.rmwinslow.com`). The main site already uses this mechanism
  for its Blog link.
- [ ] Consolidate the `mynotes` repo (currently on the `minimal-mistakes` theme
  at a separate URL) into this repo.
