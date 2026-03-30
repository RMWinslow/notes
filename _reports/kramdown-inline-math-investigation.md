# Kramdown Inline Math Investigation

Report compiled during a Claude Code session on 2026-03-29. Covers the
kramdown/MathJax inline math underscore problem, why the various proposed
solutions don't fully work, and what we settled on for the notes repo.

## The Problem

Kramdown (the markdown processor used by Jekyll) does not recognize `$...$` as
a math delimiter. Only `$$...$$` is recognized. The kramdown maintainer has
explicitly declined to add `$...$` support (kramdown issues #157, #672).

When kramdown encounters `$...$` in a markdown file, it treats the content
between the dollar signs as ordinary inline text and applies markdown parsing
rules. This means underscores inside inline math can be interpreted as emphasis
markers.

For example, `$x_1 + x_2$` on a single line contains two underscores.
Kramdown may interpret `_1 + x_` as emphasis, producing
`$x<em>1 + x</em>2$` in the HTML output. MathJax then receives mangled
content and fails to render correctly.

Display math (`$$...$$` on its own line, separated by blank lines) is not
affected because kramdown recognizes `$$` as a math delimiter and does not
parse the content inside.

## Solutions Investigated

### 1. `\(...\)` delimiters

Kramdown escapes backslashes before MathJax can process them. The `\(`
becomes a literal parenthesis in the HTML output.

**However**, `\(...\)` IS safe inside raw HTML blocks (e.g., `<table>`,
`<div>`, `<p>`) because kramdown does not process content within HTML tags.

**Verdict**: Not usable in markdown paragraphs. Safe in HTML blocks.

### 2. `$$...$$` for inline math

Kramdown distinguishes inline vs display `$$` by context: within a paragraph
it's inline, on its own line it's display. The content inside `$$` is
protected from markdown parsing.

**However**, other renderers (VS Code markdown preview, many GitHub contexts)
always treat `$$` as display math, rendering it as a centered block equation.
This breaks portability — the source no longer previews correctly outside of
Jekyll, and copying equations into LaTeX or LyX documents requires removing
the extra `$`.

**Verdict**: Works in Jekyll but breaks portability.

### 3. Escaping underscores as `\_`

Since kramdown processes inline math as markdown, `\_` is un-escaped to `_`
before MathJax sees it. The math renders correctly in Jekyll.

**However**, the source now contains `\_` which is not valid LaTeX. VS Code
previews, GitHub rendering, and copy-paste to LaTeX/LyX all show literal
underscores instead of subscripts.

**Verdict**: Works in Jekyll but breaks portability.

### 4. Kramdown configuration

There is no kramdown setting to make it recognize `$...$` as math. The
`math_engine` option (values: `mathjax`, `katex`, `nil`, etc.) only controls
what happens after kramdown has identified a math element. It does not affect
parsing.

Setting `math_engine: nil` was suggested but hits a known Jekyll bug
(jekyll#8256) that looks for a nonexistent `kramdown-math-nil` gem.

**Verdict**: No configuration-level fix exists.

### 5. Jekyll plugin (custom kramdown parser)

A custom parser class that overrides kramdown's `INLINE_MATH_START` regex to
support `$...$` is possible. An example exists in kramdown issue #672.

**However**, GitHub Pages runs Jekyll in `--safe` mode, which disables custom
plugins. This would require switching to a GitHub Actions build workflow.

**Verdict**: Would work but requires abandoning GitHub Pages' default build.

### 6. Build-time filter ($→$$ replacement)

A pre-render filter that converts `$...$` to `$$...$$` during the Jekyll
build, before kramdown processes the markdown. Authors would write portable
`$...$` in source while kramdown sees protected `$$...$$`.

This faces the same constraint as option 5: it would need to be a Jekyll
plugin, which requires GitHub Actions. There is no Liquid hook that runs
before kramdown.

**Verdict**: Same constraint as option 5.

## What We Settled On

### Line-break separation

Kramdown needs a **matching pair** of `_` on the same line to form emphasis.
A single underscore on a line cannot trigger emphasis on its own. Both
markdown and LaTeX treat a single newline within a paragraph as a space.

So we break lines to ensure no single line contains two or more underscores
across all its inline math expressions:

```markdown
Good — one underscore per line:
Consider functions $f_1(x)$
and $f_2(x)$
over the interval $[A,B]$.

Bad — two underscores on one line:
Consider functions $f_1(x)$ and $f_2(x)$ over the interval $[A,B]$.
```

Both render identically in the browser, but the first is safe from kramdown
emphasis parsing.

### HTML blocks for math-heavy sections

For sections that are naturally dense with math (like proofs), we keep them
as HTML inside a `<div>` block, using `\(...\)` delimiters. Since kramdown
does not process content within HTML tags, the math is fully insulated.

This was the approach we used for the crossing proof page's proof section,
which had too many subscripted expressions to make the line-break approach
practical for every line.

### Auditing procedure

When migrating a page:
1. Convert display math `\[...\]` to `$$...$$` on own lines — always safe
2. Convert inline math `\(...\)` to `$...$` in markdown paragraphs
3. Check whether any line has two or more underscores
4. If so, break the line so each has at most one
5. If a single expression has two or more underscores and can't be broken,
   flag it (or wrap the paragraph in an HTML block)
6. Keep math-heavy sections (proofs, theorem bodies) as HTML blocks with
   `\(...\)` delimiters

A skill file implementing this audit procedure was created at
`.claude/skills/inline-math-audit.md`.

## Key References

- [Kramdown issue #157](https://github.com/gettalong/kramdown/issues/157) —
  Processes underscores inside single dollar signs
- [Kramdown issue #672](https://github.com/gettalong/kramdown/issues/672) —
  Math block delimiter is the same for inline and display math
- [Jekyll issue #8256](https://github.com/jekyll/jekyll/issues/8256) —
  `math_engine: nil` breaks kramdown_parser
- [Kramdown syntax docs](https://kramdown.gettalong.org/syntax.html)
- [GitHub Pages dependency versions](https://pages.github.com/versions/) —
  GitHub Pages uses kramdown 2.4.0

## Future Work

The best long-term fix would be a custom kramdown parser plugin that adds
`$...$` support, deployed via a GitHub Actions build. This is tracked as a
TODO in the JTD-RMW theme repo's CLAUDE.md.
