---
description: Audit markdown files for kramdown inline math issues, and guide for writing inline math safely in Jekyll markdown.
---

# Inline math in Jekyll/kramdown

## The problem

Kramdown does not recognize `$...$` as a math delimiter. Only `$$...$$` is
recognized. When kramdown encounters `$...$` in a markdown file, it treats the
content between the dollar signs as ordinary markdown text. This means
underscores inside inline math can be interpreted as emphasis markers.

For example, `$x_1 + x_2$` on a single line contains two underscores. Kramdown
may interpret `_1 + x_` as emphasis, producing `$x<em>1 + x</em>2$` in the
HTML output. MathJax then receives mangled content and renders it incorrectly.

Display math (`$$...$$` on its own line) is not affected, because kramdown
recognizes `$$` as a math delimiter and does not parse the content inside.

## Why alternatives don't work

**`\(...\)` delimiters**: Kramdown escapes backslashes before MathJax can
process them. The `\(` becomes a literal parenthesis in the HTML. However,
`\(...\)` IS safe inside raw HTML blocks (e.g., `<table>`, `<div>`, `<p>`)
because kramdown does not process content within HTML tags.

**`$$...$$` for inline math**: Kramdown distinguishes inline vs display `$$` by
context (within a paragraph vs on its own line). This protects the math content
from markdown parsing. However, other renderers (VS Code markdown preview,
many GitHub contexts) always treat `$$` as display math, rendering it as a
centered block equation. This breaks portability — the source no longer
previews correctly outside of Jekyll, and copying equations into LaTeX or LyX
documents requires removing the extra `$`.

**Escaping underscores as `\_`**: Kramdown un-escapes `\_` to `_` before
MathJax sees it, so the math renders correctly in Jekyll. But the source now
contains `\_` which is not valid LaTeX. VS Code previews, GitHub rendering,
and copy-paste to LaTeX/LyX all break.

**Kramdown configuration**: There is no kramdown setting to make it recognize
`$...$` as math. The maintainer has explicitly declined to add one (kramdown
issues #157, #672). The `math_engine` option only affects output format, not
parsing.

**Jekyll plugins**: A custom kramdown parser that adds `$...$` support is
possible (see kramdown issue #672 for an example), but GitHub Pages runs in
safe mode which blocks custom plugins. Switching to a GitHub Actions build
workflow would allow this.

## The recommended approach: line-break separation

Kramdown needs a **matching pair** of `_` on the same line to form emphasis.
A single underscore on a line cannot trigger emphasis on its own.

Both markdown and LaTeX treat a single newline within a paragraph as a space.
So we can break lines to ensure no single line contains two or more underscores
across all its inline math expressions:

```markdown
Good — one underscore per line:

Consider functions $f_1(x)$
and $f_2(x)$
over the interval $[A,B]$.

Bad — two underscores on one line:

Consider functions $f_1(x)$ and $f_2(x)$ over the interval $[A,B]$.
```

Both render identically, but the first is safe from kramdown emphasis parsing.

### When line-breaking isn't enough

If a single inline math expression contains two or more underscores (e.g.,
`$x_1 + x_2$`), it cannot be split across lines. Options for these cases:

1. **Rewrite as two expressions**: `$x_1$ and $x_2$` (if the context allows)
2. **Use display math**: put the expression in `$$...$$` on its own line
3. **Wrap in HTML**: `<span>$x_1 + x_2$</span>` may protect the content,
   though this is not guaranteed for inline HTML elements in all kramdown
   versions
4. **Accept the risk**: mid-word underscores (like `x_1`) often don't trigger
   emphasis because kramdown requires flanking delimiters at word boundaries.
   Test the output and flag if it breaks.

## Future fix: build-time filter

The cleanest long-term solution would be a pre-render filter in the Jekyll
build pipeline that replaces `$...$` with `$$...$$` before kramdown processes
the markdown. This would let authors write portable `$...$` in source while
kramdown sees protected `$$...$$`. This requires either:

- A Jekyll plugin (needs GitHub Actions build, not vanilla GitHub Pages)
- A pre-commit hook that generates build-ready copies
- A client-side JavaScript fix in the theme (fragile, repairs after damage)

This is tracked as a TODO in the JTD-RMW theme repo and in this repo's
CLAUDE.md.

## Auditing a file for potential issues

When migrating an HTML file to Jekyll markdown, or when reviewing an existing
markdown file for inline math safety:

1. Identify all lines that will contain inline `$...$` math after conversion
2. Check whether any single line would have two or more underscores across all
   its inline math expressions
3. If so, insert line breaks to separate expressions onto different lines
4. Check whether any single expression contains two or more underscores
5. Flag those expressions — they may need one of the workarounds above
6. Verify the rendered output after conversion
