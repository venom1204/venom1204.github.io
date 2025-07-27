---
layout: post
title: "GSoC Weeks 7–8 Progress: Friendlier Errors, Discoverable Helpers, and ISO Calendar Support"
subtitle: "Refining the Edges — From Error Messaging to Practical Utilities"
date: 2025-07-27
---

### Consistent and Clear: Unifying `:=` Error Messages (PR in Progress, [#4920](https://github.com/Rdatatable/data.table/issues/4920))

I improved error messaging for `:=` misuse inside `{}` blocks:

- Updated the main `stopf()` messages in `R/data.table.R` to **clarify the rules**:
  - "`:=` must be the only statement inside `{}` and may only appear once."
  - Suggests using `{}` on the RHS of `:=` for multi-step logic.
- Enhanced the general `:=` error to **hint at common mistakes** (like using `<-` or multiple statements).
- Added a **note in `assign.Rd`** explaining that `:=` inside `{}` must be the only statement, pointing users toward the functional form for multi-column updates.

These changes make the error messages **clearer and more instructive**, reducing confusion for new users.

---

### Making New Helpers Discoverable: `cbindlist()` and `mergelist()` Examples (PR in Progress, [#7171](https://github.com/Rdatatable/data.table/issues/7171))

I added **concise examples** to `NEWS.md` for the new helper functions:

- `cbindlist()`: shows a basic column-wise concatenation of two `data.table`s from a list.
- `mergelist()`: demonstrates both **recursive inner join** and **left join** on a shared `id` key.

These examples give users a quick understanding of the new functions directly from the release notes, without needing to dive into full documentation.

---

### Smoother Onboarding: Example for `sort_by()` (PR [#7196](https://github.com/Rdatatable/data.table/pull/7196), Closes [#7140](https://github.com/Rdatatable/data.table/issues/7140))

The new `sort_by()` API makes it easy to reorder data by custom conditions, but without examples, its power is less obvious.

To address this:

- I added a **clear, minimal usage example** to `NEWS.md`, so readers can grasp its purpose immediately.
- The example complements full documentation, helping first-time users get started quickly.

---

### Strengthening Date Support: Adding `isoyear()` (PR [#7197](https://github.com/Rdatatable/data.table/pull/7197), Closes [#7154](https://github.com/Rdatatable/data.table/issues/7154))

Many workflows rely on ISO calendars, and while `data.table` already had `isoweek()`, there was no direct way to extract the **ISO year**.

To close this gap:

- I implemented a **fast, base-R–wrapped function** in `R/IDateTime.R`:

  ```r
  isoyear = function(x) as.integer(format(as.IDate(x), "%G"))
