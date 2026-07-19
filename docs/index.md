---
hide:
  - navigation
  - toc
---

# RegTab

**Turn tables made for people into machine-readable records.**

RegTab is a data-wrangling toolkit for tables designed for reading rather
than querying — spreadsheets, cross-tabs and reports with hierarchical
headers and compound cells. At its core is RTL (Regular Table Language),
a pattern DSL that does for tables what regular expressions do for strings:
a pattern describes the table's repeating layout and how the matched cells
map to attributes, values and records.

## Tools

<div class="project-grid" markdown>

<div class="project-card" markdown>
### jRegTab
The reference implementation of RegTab in Java. Use RTL as a standalone
or embedded DSL.

<div class="card-actions">
  <a class="md-button md-button--primary" href="https://regtab.github.io/jregtab/">Documentation</a>
  <a class="md-button" href="https://github.com/regtab/jregtab">Repository</a>
</div>
</div>

<div class="project-card" markdown>
### pyRegTab
A Python port of jRegTab; extracted record sets convert straight to
pandas DataFrames.

<div class="card-actions">
  <a class="md-button md-button--primary" href="https://regtab.github.io/pyregtab/">Documentation</a>
  <a class="md-button" href="https://github.com/regtab/pyregtab">Repository</a>
</div>
</div>

<div class="project-card" markdown>
### vscode-rtl
Full RTL support in VS Code: highlighting, as-you-type diagnostics and
completion, and live match preview against sample tables.

<div class="card-actions">
  <a class="md-button md-button--primary" href="https://github.com/regtab/vscode-rtl">Repository</a>
</div>
</div>

<!--
  Card template for the next tool — copy the block above,
  then change the name, description and links.
  Note: write the buttons as raw <a> tags (no `markdown` attribute on
  .card-actions) so Markdown does not wrap them in a <p>.

<div class="project-card" markdown>
### Tool name
A short one- or two-line description.

<div class="card-actions">
  <a class="md-button md-button--primary" href="https://regtab.github.io/repository-name/">Documentation</a>
  <a class="md-button" href="https://github.com/regtab/repository-name">Repository</a>
</div>
</div>
-->

</div>

## How it works

Take this cross-tab of airline on-time data: airlines across the top,
airports down the side, and compound cells like `31 Jan` holding two
values — a number and a month:

|     | CA     | HU     |
|-----|--------|--------|
| IKT | 0 Jan  | 8 Feb  |
| SVO | 31 Jan | 40 Feb |

This RTL pattern mirrors the layout — a header row of airlines, then
repeated airport rows — and tells how the matched cells map to attributes
(`->AVP`) and records (`->REC`):

```text
[ [] [VAL : 'AIRLINE'->AVP]+ ]
[ [VAL : 'AIRPORT'->AVP]
  [VAL : (COL, ROW, CL)->REC, 'ND'->AVP " " VAL : 'MON'->AVP]+ ]+
```

Matching it against the table unpivots the cross-tab into a flat record
set — one record per data cell, ready for a DataFrame or CSV:

| ND | AIRLINE | AIRPORT | MON |
|----|---------|---------|-----|
| 0  | CA      | IKT     | Jan |
| 8  | HU      | IKT     | Feb |
| 31 | CA      | SVO     | Jan |
| 40 | HU      | SVO     | Feb |
