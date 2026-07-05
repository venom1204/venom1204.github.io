---
layout: post
title: "GSoC Sixth Week Progress"
subtitle: "Improving print.data.table() and .SD Diagnostics"
date: 2026-07-05
tags: [gsoc2026]
---

### Fixing `print.data.table()` Edge Cases

This week I focused on improving the behavior of `print.data.table()` by addressing [issue #7735](https://github.com/Rdatatable/data.table/issues/7735).

The issue occurred when `col.names="none"` was used together with `row.names=FALSE`. Instead of printing the data without column headers, `print.data.table()` produced no output at all.

To resolve this, I submitted [PR #7804](https://github.com/Rdatatable/data.table/pull/7804), which changes the internal handling when row names are suppressed. Rather than relying on a pattern that expected row markers, the header is now removed by position, ensuring that the data rows are printed correctly.

### Improving `.SD` Diagnostics

I also worked on [issue #7431](https://github.com/Rdatatable/data.table/issues/7431), which highlighted confusion caused by local assignments to columns that are included in `.SD`.

Initially, the discussion focused on improving the documentation, but after further feedback the solution evolved into warning users whenever local assignments to `.SD` columns are detected.

I submitted [PR #7807](https://github.com/Rdatatable/data.table/pull/7807), which includes:

- A recursive scanner to detect local writes to columns referenced by `.SD` while avoiding false positives from read operations.
- Documentation updates explaining the behavior of `.SD` and the new warning.
- Regression tests covering grouped, ungrouped, and false-positive scenarios.

This work helps make `.SD` behavior more explicit while preserving existing workflows.

### Looking Ahead

With these improvements completed, I'll continue working on documentation and consistency improvements across `data.table`, while following up on review comments for the open pull requests.
```
