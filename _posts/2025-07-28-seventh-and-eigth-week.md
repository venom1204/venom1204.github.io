---
layout: post
title: "GSoC Weeks 7–8 Progress: Friendlier Errors, Discoverable Helpers, and ISO Calendar Support"
subtitle: "Refining the Edges — From Error Messaging to Practical Utilities"
date: 2025-07-27
---

### Consistent and Clear: Unifying `:=` Error Messages (In Progress, [#4920](https://github.com/Rdatatable/data.table/issues/4920))

One of the recurring user pain points in `data.table` has been **confusing and inconsistent errors** when using `:=` inside `{}` blocks.  
Two separate error messages existed:

1. When users placed multiple `:=` calls inside `{}`.
2. When extra expressions were mixed in alongside `:=`.

These messages were **worded differently**, forcing users to read through `?":="` or examples to understand the rules.

To simplify this:

- I analyzed the **existing error-checking logic**, which only inspects the **first statement** inside `{}`.  
  This caused cases like `{ tmp = 1; (tmp) := 2 }` to **fall through** to a generic, unhelpful message.
- I refactored the handling so **all lines in the `{}` block are scanned** for `:=`, ensuring both types of misuse are caught consistently.
- Introduced a **single, unified error message**:

  > “You have wrapped `:=` with `{}`, which is allowed, but `:=` must be the only expression inside `{}` and may only appear once.  
  > Consider placing the `{}` on the RHS of `:=`, e.g. `DT[, col := { tmp1 <- ...; tmp2 <- ...; tmp1 * tmp2 }]`. See `?":="` for details.”

- Planned updates to `?":="` and `?data.table` to **highlight this rule prominently** so users don’t need to read the entire help page to discover it.

This work brings consistency, improves guidance, and helps beginners avoid common frustrations when dynamically updating columns.

---

### Quick Demos for New Helpers: `cbindlist()` and `mergelist()` (Ongoing, [#7171](https://github.com/Rdatatable/data.table/issues/7171))

The release introduces two convenience functions:

- **`cbindlist()`**: column-binds a list of `data.table`s into one.
- **`mergelist()`**: performs recursive merges across a list, supporting `how = "inner"` and `"full"` joins on a shared key.

To make these discoverable without requiring users to read the full manuals:

- I drafted **concise examples** for `NEWS.md`:
  - `cbindlist()`: a minimal column-wise concatenation demo.
  - `mergelist()`: both inner and full joins on a shared `id`.
- These examples act as **quick teasers**, encouraging readers to explore the full help pages if they need more.

This ensures users can quickly understand new tools right from the release notes.

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
