---
layout: post
title: "GSoC Progress Update"
subtitle: "Feature Development, Documentation Improvements, and Review Iterations"
date: 2026-07-26
tags: [gsoc2026]
---

Over the past three weeks, my development pace slowed temporarily as I was in the process of reorganizing my work environment and subsequently recovering from a fever. Although this reduced the amount of time I could dedicate to development, I continued making steady progress across multiple tasks. I have now fully resumed work and am back to my usual pace. During this period, I worked on several feature requests, documentation improvements, and review iterations across different areas of **data.table**.

## Improving `.SD` Diagnostics

One of my major contributions during this period was addressing [issue #7431](https://github.com/Rdatatable/data.table/issues/7431), which highlighted confusion caused when `.SD` returns its original snapshot even after local assignments are made to columns inside `j`.

The discussion initially focused on improving the documentation. However, after maintainer feedback, the proposed solution evolved into warning users whenever local assignments are made to columns that are included in `.SD`. This approach preserves existing behavior while making the underlying semantics much more explicit.

I submitted [PR #7807](https://github.com/Rdatatable/data.table/pull/7807), which includes:

- A recursive scanner in `R/data.table.R` that detects writes to columns referenced by `.SD` while ignoring read-only operations.
- Scope-sensitive warnings that correctly handle nested `data.table` expressions.
- Documentation updates to `special-symbols.Rd` and the `.SD` vignette explaining the static snapshot behavior of `.SD`.
- Regression tests covering grouped, ungrouped, nested, and false-positive scenarios.

During review, I also addressed maintainer feedback regarding implementation details, test conventions, issue references, and overall behavior in nested expressions.

## Adding `limit` Support to `nafill()` and `setnafill()`

I also worked on [issue #7677](https://github.com/Rdatatable/data.table/issues/7677), which proposed adding a way to restrict the number of consecutive missing values filled during LOCF (Last Observation Carried Forward) and NOCB (Next Observation Carried Backward) operations.

I submitted [PR #7819](https://github.com/Rdatatable/data.table/pull/7819), introducing a new `limit` argument to both `nafill()` and `setnafill()`.

The implementation includes:

- A new `limit = Inf` argument that preserves existing behavior by default.
- Updates to both the R interface and the underlying C implementation for efficient support of LOCF and NOCB.
- Documentation updates with practical usage examples.
- Regression tests covering the new functionality.

The review process generated several valuable suggestions, including additional validation for edge cases such as zero, negative, fractional, `NA`, `NaN`, `NULL`, complex values, vectors of length greater than one, `type="const"`, by-reference behavior in `setnafill()`, and NEWS updates. I am currently incorporating this feedback to strengthen the implementation before merge.

## Extending `setnafill()` with Logical Column Selection

I also worked on [issue #4113](https://github.com/Rdatatable/data.table/issues/4113), which requested support for logical vectors in the `cols` argument of `setnafill()`. Previously, users had to manually convert logical selections into column names or indices before passing them to `setnafill()`. Supporting logical vectors allows users to write more natural and concise code, such as `sapply(DT, is.numeric)`, when selecting columns for in-place missing value filling.

To address this, I submitted [PR #7842](https://github.com/Rdatatable/data.table/pull/7842), which extends `setnafill()` to natively accept logical vectors for the `cols` argument while maintaining full compatibility with the existing API.

The implementation includes:

- Extending `setnafill()` to accept logical vectors in addition to integer and character column specifications.
- Updating the internal `colnamesInt` C utility to recognize and process logical vectors efficiently.
- Validating that supplied logical vectors have the exact length as the number of columns in the `data.table`.
- Rejecting logical vectors containing `NA` values to ensure predictable behavior.
- Preserving the package's existing error-handling logic so that validation remains consistent across all APIs relying on `colnamesInt`.
- Adding regression tests covering valid logical selections along with error cases involving incorrect lengths and missing (`NA`) values.

This enhancement improves the usability of `setnafill()` by enabling dynamic, condition-based column selection while keeping the implementation efficient and fully consistent with the existing behavior of **data.table**.

## Clarifying `R CMD check` NOTES for the `..` Prefix

Another contribution during this period focused on improving the documentation for [issue #4741](https://github.com/Rdatatable/data.table/issues/4741), which concerns the `R CMD check` NOTE generated when using the `..` prefix inside R packages.

I submitted [PR #7826](https://github.com/Rdatatable/data.table/pull/7826), which:

- Explains why `..` variables trigger an `R CMD check` NOTE.
- Documents recommended approaches using `globalVariables()`, `with=FALSE`, and the newer `env=` interface.
- Adds guidance for package developers in the programming and importing vignettes.
- Improves examples and documentation throughout the affected pages.

Following review, I refined the documentation further by incorporating maintainer suggestions regarding nested expressions and the appropriate use of the `env=` argument. The pull request has since received approvals after the requested refinements.

## Improving `print.data.table()` Console Width Handling

I also continued work on [issue #7797](https://github.com/Rdatatable/data.table/issues/7797), which focuses on ensuring long column names do not exceed the available console width in `print.data.table()`.

To simplify the development process after resolving issues with the previous branch, I opened a new pull request, [PR #7830](https://github.com/Rdatatable/data.table/pull/7830).

This update:

- Truncates long column headers using the existing `char.trunc()` logic.
- Ensures the "variables not shown" footer also respects the configured console width.
- Preserves backward compatibility when `datatable.prettyprint.char = Inf`.
- Includes regression tests covering multiple printing scenarios.

During review, maintainers also shared valuable guidance on Git workflows and pull request management. This feedback has helped me improve how I manage feature branches and organize future contributions.

## Adding Reverse Indexing to `tstrsplit()`

Finally, I began work on [issue #6341](https://github.com/Rdatatable/data.table/issues/6341), which proposes reverse indexing support for `tstrsplit()`.

I submitted [PR #7838](https://github.com/Rdatatable/data.table/pull/7838), introducing a new `rev` argument.

The new feature:

- Enables component extraction relative to the end of a string.
- Simplifies parsing strings containing a variable number of delimiters.
- Allows users to directly extract the last or second-to-last components without manually reversing vectors.
- Includes documentation updates and regression tests covering the new functionality.

The implementation is currently under review, and I will continue refining it based on maintainer feedback.

## Looking Ahead

Over the coming weeks, my primary focus will be on addressing review comments for the currently open pull requests, expanding regression test coverage where needed, and refining both the implementation and documentation of recently added features. As these contributions move toward merge readiness, I also plan to continue working on additional feature requests and documentation improvements to further enhance the usability, consistency, and overall developer experience of **data.table**.
