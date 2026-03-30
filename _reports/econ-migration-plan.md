# Economics Notes Migration Plan

Report compiled during a Claude Code session on 2026-03-29. Documents the
planned migration of legacy HTML economics content into the Jekyll nav tree.

## Current State

The notes repo (`www.rmwinslow.com/notes/`) has three kinds of economics
content:

1. **Already migrated to Jekyll markdown**: `302/` (Intermediate Macro, ~20+
   pages), `202/` (Principles of Macro, 1 page), `typesetting/` (3 pages).

2. **Legacy HTML, served but not in nav**: `econ/` (~65 HTML files without
   frontmatter), `_detritus/research/arrowroot/` (3 HTML files + 1 PDF).

3. **Unindexed teaching content**: `econ/teaching/3102/` (interactive
   walkthroughs, possibly superseded by 302/), `econ/teaching/3102psets/`
   (problem set data graphs), `econ/presentations/` (percolation slides).

## Target Nav Structure

We decided on Variant C from the brainstorming session: topic-based within
each exam section, with pages ordered by professor and professor attribution
as metadata on each page.

```
UMN Prelims
├── Macro
│   ├── Cash-Credit and Private Money          (Chari)
│   ├── Sustainable Debt and Ramsey            (Chari)
│   ├── McCall Search                          (Kehoe)
│   ├── Crossing Proof                         (Kehoe)
│   ├── Dynamic Programming                    (Jones)
│   ├── Human Capital Growth                   (Jones)
│   ├── Envelope Condition
│   └── Flowchart Key
├── Trade
│   ├── Dynamic Heckscher–Ohlin                (Amador / Kehoe)
│   ├── Armington and Gravity                  (Fitzgerald)
│   ├── Melitz–Ottaviano                       (Fitzgerald)
│   ├── Monopolistic Competition               (Kehoe)
│   ├── Self-Fulfilling Debt Crises            (Kehoe)
│   └── Learning by Doing                      (Kehoe)
└── Micro
    ├── Arrow's Theorem
    └── Root's Mechanisms
```

Parent pages have been created at:
- `prelim/index.md` (UMN Prelims)
- `prelim/macro/index.md` (Macro Prelim)
- `prelim/trade/index.md` (Trade Prelim)
- `prelim/micro/index.md` (Micro Prelim)

The user noted that the URL depth (`/notes/prelim/macro/crossing-proof`) is
undesirably long. This may be revisited.

## File Inventory and Status

A detailed inventory with per-file migration and completion status is
maintained in `econ-index.md` at the repo root. Summary below.

### Macro prelim — ready to migrate

| Source file | Topic | Status |
|-------------|-------|--------|
| Chari/privatemoney.html | Cash-credit with private money | Complete |
| Chari/sustainabledebt.html | Sustainable debt and Ramsey | Complete |
| Kehoe/Search.html | McCall search model | Complete |
| Kehoe/crossingProof.html | Crossing proof lemma | **Migrated** |
| Concepts/envelope.html | Envelope condition | Complete |
| Concepts/flowchartkey/FlowChartKey.html | Flowchart notation key | Complete |

### Macro prelim — needs work before migration

| Source file | Topic | Status |
|-------------|-------|--------|
| Jones/dynamicprogramming.html | DP in one-sector growth | Partial (TODO at end, duplicate search content) |
| Jones/HumanCapital.html | Human capital growth | Partial (proof trails off, duplicate search content) |
| Chari/productionrisk.html | Production risk | Stub |

### Macro prelim — duplicates and junk (delete or skip)

- Kehoe/dp.html — exact duplicate of Search.html
- Jones/questions.txt — one-line question
- macroprelim/roadmapTODO.html — layout experiments
- macroprelim/prelimindex.html — superseded by Jekyll nav parent

### Trade prelim — ready to migrate

| Source file | Topic | Status |
|-------------|-------|--------|
| amador/multipleborrowers.html | Dynamic Heckscher–Ohlin | Complete |
| fitzgerald/armingtongravity.html | Armington and gravity | Complete |
| fitzgerald/melitzottaviano_solution.html | Melitz–Ottaviano | Nearly complete (some TODOs) |
| kehoe/hecksherohlin.html | Heckscher–Ohlin | Complete |
| kehoe/monopolisticcompetition.html | Monopolistic competition | Complete |
| kehoe/self-fulfillingdebt.html | Self-fulfilling debt | Complete |
| kehoe/LBD/LBDprelimSolutionA.html | Learning by doing | Complete |

### Trade prelim — problem statements only

| Source file | Topic |
|-------------|-------|
| fitzgerald/melitzottaviano.html | Melitz–Ottaviano problem |
| kehoe/LBD/LBDprelim.html | LBD problem |

### Trade prelim — duplicates, junk, scratchwork

- fitzgerald/melitzottaviano_problem.html — duplicate
- fitzgerald/melitzottaviano/melitzottaviano.html — duplicate
- fitzgerald/mellitz work.lyx — scratchwork
- kehoe/hecksherwork.lyx — scratchwork
- kehoe/debtcrisiswork.lyx — empty
- kehoe/learningbydoing.html — stub, superseded by LBD/
- kehoe/LBD/LBDconcepts.html — empty
- tradeprelim/prelimindex.html — superseded by nav parent

### Micro prelim (Arrow/Root)

| Source file | Topic | Status |
|-------------|-------|--------|
| arrowrootnotes.html | Root's mechanisms, GS proof | Complete |
| arrownotes.html | Arrow's theorem | Partial (tangents mixed in) |
| Root - Incentive Stuff.pdf | Root's paper | Reference PDF |

### Planned but never written

From the original index files:
- **Chari**: Search and Unemployment, Default and Gov Debt
- **Kehoe**: Overlapping Generations, Sequential Markets vs Arrow-Debreu
- **Jones**: Entire section was empty in the index
- **Amador**: Defaults, Multiple Borrowers, and Safe Assets (2019s)

## Migration Workflow

Established by migrating the crossing proof page (the first test case):

1. **Create the markdown file** in `prelim/<section>/` with frontmatter:
   `title`, `parent`, `grand_parent`, `math: mathjax`, `nav_order`,
   `redirect_from` (for the old URL).

2. **Convert display math** `\[...\]` to `$$...$$` on own lines. Always safe.

3. **Convert inline math** `\(...\)` to `$...$` in markdown paragraphs.
   Break lines so no single line has two or more underscores. See the
   kramdown inline math investigation report for details.

4. **Keep math-heavy sections as HTML blocks** inside `<div>` tags, using
   `\(...\)` delimiters. This insulates the math from kramdown parsing and
   preserves tight line spacing (using `<br>` tags).

5. **Copy images** to `prelim/<section>/img/`.

6. **Add redirect_from** in the new page's frontmatter for the old
   `/notes/econ/...` URL.

7. **Update the main repo's redirect stub** to point directly to the new URL
   (keeping the redirect from the original pre-migration URL as single-hop).

8. **Update econ-index.md** — mark the file as migrated.

## CSS

We created `assets/css/extrabits.css` with styling for the `.definition`
class, using the JTD-RMW theme's CSS variables (`--boxcolor`, `--accentcolor`,
`--feedbackcolor`). This gives theorem/definition boxes a cream background
with a maroon border, matching the original sakura CSS styling.

## Open Questions

- **URL depth**: The three-level nesting (`/prelim/macro/page`) is long. Could
  flatten to two levels but would lose the exam-section grouping in the URL.
- **What to do with the problem-only files**: Merge them into the solution
  pages? Keep them separate?
- **The Jones duplicates**: The search problem content is triplicated across
  Jones/HumanCapital.html, Jones/dynamicprogramming.html, and
  Kehoe/Search.html. The unique content (DP, human capital) needs to be
  extracted and the search duplicate discarded.
- **Unindexed content**: econ/teaching/3102/, econ/teaching/3102psets/, and
  econ/presentations/ have not been inventoried yet. The teaching/3102/
  content may be superseded by 302/.
- **Post-migration polish**: After all pages are migrated, add related links
  between pages, references to seminal papers, and other contextual material
  (tracked as a TODO in CLAUDE.md).

## Commits Made

1. `b759a75` — Create econ-index.md
2. `b5f4401` — Index legacy econ files for migration planning
3. `b2d34f1` — Add planning and scaffolding for the UMN Prelims nav section
4. `023b095` — Migrate the crossing proof page and document the inline math issue
5. `4473fa9` — Fix the crossing proof spacing and add definition box styling
