# GSOC Final Submission

## Getting Started
My GSoC journey began with a deep interest in contributing to **data.table**, one of the most powerful and widely used R packages for data manipulation. At the start, I familiarized myself with the codebase, community practices, and identified areas where improvements could be made. With the constant guidance of my mentors, I quickly transitioned into actively contributing.

## The Work
Over the course of the program, I worked on a variety of issues ranging from documentation improvements, bug fixes, refining error messages, and adding new functionalities to the package. Each contribution, whether small or large, gave me valuable insights into maintaining a large-scale open-source project and writing user-friendly, efficient, and reliable code.

### Pull Requests Contributed During GSoC

| PR Title                                                                                                         | Link                                                                 |
|------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| Relax fwrite `dec == sep` restriction for single-column input                                                    | [#7233](https://github.com/Rdatatable/data.table/pull/7233)          |
| Added fwrite and fread vignette                                                                                  | [#7216](https://github.com/Rdatatable/data.table/pull/7216)          |
| Added isoyear function                                                                                           | [#7197](https://github.com/Rdatatable/data.table/pull/7197)          |
| Added example of sort_by in the news                                                                             | [#7196](https://github.com/Rdatatable/data.table/pull/7196)          |
| Updated := error message                                                                                         | [#7188](https://github.com/Rdatatable/data.table/pull/7188)          |
| Fixed outdated example in reshape vignette                                                                       | [#7150](https://github.com/Rdatatable/data.table/pull/7150)          |
| Fix: Ensure column widths are data-driven when `col.names = "none"` in `print.data.table`                        | [#7130](https://github.com/Rdatatable/data.table/pull/7130)          |
| Suppressed spurious min/max warnings in cube() internal structure-seeding eval()                                 | [#7110](https://github.com/Rdatatable/data.table/pull/7110)          |
| Handle get0() in setDT() to preserve .internal.selfref                                                           | [#7101](https://github.com/Rdatatable/data.table/pull/7101)          |
| Sequence correction                                                                                              | [#7081](https://github.com/Rdatatable/data.table/pull/7081)          |
| Refactored duplicate recursive assignment logic in `[.data.table` and `setDT` into shared helper                 | [#7064](https://github.com/Rdatatable/data.table/pull/7064)          |
| Clarified behavior of "24:00:00" in as.ITime()                                                                   | [#7057](https://github.com/Rdatatable/data.table/pull/7057)          |
| Clarified setindex vs setkey subsetting behavior                                                                 | [#7047](https://github.com/Rdatatable/data.table/pull/7047)          |
| Enhanced setDT Documentation: Added Example for RDS/RData Usage and FAQ Link                                     | [#6894](https://github.com/Rdatatable/data.table/pull/6894)          |
| Fix: Added Examples of Named List Elements in i to Improve Clarity                                               | [#6868](https://github.com/Rdatatable/data.table/pull/6868)          |
| Combine DTPRINT statements for fread verbose messages                                                            | [#6848](https://github.com/Rdatatable/data.table/pull/6848)          |
| Simplified and Extended "Updating by Reference" Section in Joins Vignette                                        | [#6847](https://github.com/Rdatatable/data.table/pull/6847)          |
| Improved Non-Equi Join Explanation in data.table                                                                 | [#6813](https://github.com/Rdatatable/data.table/pull/6813)          |
| Fix typo in join vignette: Replace "banana" with "soda"                                                          | [#6801](https://github.com/Rdatatable/data.table/pull/6801)          |
| Improve merge.data.table error messages for missing keys                                                         | [#6713](https://github.com/Rdatatable/data.table/pull/6713)          |
| Add example of `cols=<list>` to ?setindexv                                                                       | [#6678](https://github.com/Rdatatable/data.table/pull/6678)          |
| Warn when by/keyby is used with column selection via character or numeric j                                      | [#7254](https://github.com/Rdatatable/data.table/pull/7254)          |
| rowwise(): Detect and reject non-atomic, non-list column values with clear error message                         | [#7250](https://github.com/Rdatatable/data.table/pull/7250)          |
| Added examples for cbindlist and mergelist                                                                       | [#7172](https://github.com/Rdatatable/data.table/pull/7172)          |
| tables() supports recursive search for nested data.tables via recursive=TRUE argument                            | [#7141](https://github.com/Rdatatable/data.table/pull/7141)          |
| Updated bmerge() to support joins on complex columns with zero imaginary part, treating them as double           | [#7085](https://github.com/Rdatatable/data.table/pull/7085)          |
| Fixed week() calculation to start week 1 at days 1–7                                                             | [#7274]
(https://github.com/Rdatatable/data.table/pull/7274)          |

## Overall Experience
This journey has been both exciting and transformative. I gained not only technical skills in R, data.table internals, and collaborative software development but also learned the importance of communication, community engagement, and iterative problem-solving. Every PR review from my mentors helped me improve, and the encouragement I received from the community kept me motivated throughout.

## Word of Thanks
I would like to sincerely thank my mentors and the **R Project for Statistical Computing** community for their continuous support, guidance, and encouragement. Their patience, expertise, and constructive feedback made this experience truly enriching.  

## Looking Ahead
My GSoC journey might be concluding, but my involvement with the R Project and data.table is far from over. I look forward to continuing my contributions, exploring more challenging issues, and being an active part of this vibrant open-source community in the future.  
