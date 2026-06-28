---
layout: post
title: "GSoC Fourth & Fifth Week Progress"
subtitle: "Improving Printing Behavior and API Consistency in data.table"
date: 2026-06-28
tags: [gsoc2026]
---

### Focusing on Print Improvements and Consistency

Over the fourth and fifth weeks of the coding period, I focused primarily on improving the printing experience in `data.table`. These contributions ranged from enhancing `print.data.table()` with new functionality to fixing inconsistencies in date conversion methods.

### Optional Column Count Display in `print.data.table()` (Issue [#6663](https://github.com/Rdatatable/data.table/issues/6663), PR [#7791](https://github.com/Rdatatable/data.table/pull/7791))

The first contribution was implementing an optional way to display the total number of columns when printing a data table.

The implementation introduces:
- A new global option, `datatable.show.ncols`
- A corresponding `show.ncols` argument in `print.data.table()`

When enabled, the total column count is displayed in the header. The feature also integrates with `trunc.cols=TRUE`, reporting both the total number of columns and how many are hidden due to width limitations.

The goal was to make wide tables easier to interpret while keeping the feature optional for users who prefer the existing output.

### Preserving Names in `as.IDate()` and `as.ITime()` (Issue [#7252](https://github.com/Rdatatable/data.table/issues/7252), PR [#7800](https://github.com/Rdatatable/data.table/pull/7800))

Another contribution focused on improving consistency between `data.table` and base R.

Previously, `as.IDate()` and `as.ITime()` dropped vector names during conversion, unlike `as.Date()`. The implementation updates the relevant conversion methods to preserve names, making their behavior consistent with base R while maintaining existing functionality.

This improves consistency and produces more predictable behavior for users working with named vectors.

### Width-Based Truncation for Long Column Names (Issue [#7797](https://github.com/Rdatatable/data.table/issues/7797), PR [#7802](https://github.com/Rdatatable/data.table/pull/7802))

I also worked on improving how `print.data.table()` handles very long column names.

Previously, long column names could exceed the available console width in both the table header and the hidden-column summary printed when `trunc.cols=TRUE`.

The implementation applies the existing width-aware truncation logic consistently across these locations so that printed output better respects the user's console width while remaining readable.

### Ongoing Work

Alongside these PRs, I also continued working on documentation improvements for the joins vignette (Issue [#662](https://github.com/Rdatatable/data.table/issues/662)), specifically around examples using the `x.` prefix in joins.

While working on the implementation, I ran into an issue that required additional investigation. I'm currently working through it and plan to submit a PR once the remaining problem is resolved.

---

These two weeks were centered around improving usability, consistency, and the overall printing experience in `data.table`. Along with implementing new features, I also spent time refining existing behavior to better align with user expectations and base R conventions.
