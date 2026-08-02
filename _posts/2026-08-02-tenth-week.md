---
layout: post
title: "GSoC 10th Week Progress"
subtitle: "Enhancing setorderv() and frank()"
date: 2026-08-02
tags: [gsoc2026]
---

### Inferring Column Names in `setorderv()`

This week I worked on improving the usability of `setorderv()` by addressing [issue #6932](https://github.com/Rdatatable/data.table/issues/6932).

Previously, when using a named `order` vector, users still had to explicitly provide the corresponding `cols` argument, resulting in redundant specification of column names.

To resolve this, I submitted [PR #7861](https://github.com/Rdatatable/data.table/pull/7861), which allows `setorderv()` to automatically infer column names from a named `order` vector when `cols` is omitted.

The implementation includes:

- Automatic inference of column names from the names of the `order` vector.
- Validation to detect duplicate names in the order mapping.
- Documentation updates and regression tests covering the new behavior.

This enhancement simplifies the API while remaining fully backward compatible.

### Supporting Reverse Ranking in `frank()`

I also worked on [issue #5489](https://github.com/Rdatatable/data.table/issues/5489), which requested support for reverse ranking directly in `frank()`.

I submitted [PR #7874](https://github.com/Rdatatable/data.table/pull/7874), bringing `frank()` into parity with `frankv()` by adding an `order` argument and supporting expressions such as `frank(-x)`.

The implementation includes:

- A new `order` argument matching the behavior of `frankv()`.
- Internal interception of the unary minus operator, allowing reverse ranking for types such as `Date` and `character`, where R does not define unary `-`.
- Regression tests covering multiple data types and ranking methods.

This makes reverse ranking more intuitive while preserving the existing interface.

### Documentation Improvements

Alongside these feature contributions, I am also working on several documentation improvements and fixes across the project. I updated examples and documentation based on reviewer feedback to improve clarity, consistency, and maintainability.

### Looking Ahead

Next, I'll continue addressing review comments on the open pull requests, refining the associated tests and documentation, and working on additional improvements to `data.table`.
