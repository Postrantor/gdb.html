---
description: List (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: List (Debugging with GDB)
lang: en
resource-type: document
title: List (Debugging with GDB)
---
::: header
Next: [Location Specifications](Location-Specifications.html#Location-Specifications)]
:::

---

### 9.1 Printing Source Lines

To print lines from a source file, use the `list` command (abbreviated `l`). By default, ten lines are printed. There are several ways to specify what part of the file you want to print; see [Location Specifications](Location-Specifications.html#Location-Specifications), for the full list.

Here are the forms of the `list` command most commonly used:

`list linenum`

:   Print lines centered around line number `linenum` in the current source file.

`list function`

:   Print lines centered around the beginning of function `function`.

`list`

:   Print more lines. If the last lines printed were printed with a `list` command, this prints lines following the last lines printed; however, if the last line printed was a solitary line printed as part of displaying a stack frame (see [Examining the Stack](Stack.html#Stack)), this prints lines centered around that line.

`list -`

:   Print lines just before the lines last printed.

By default, [GDB] prints ten source lines with any of these forms of the `list` command. You can change this using `set listsize`:

`set listsize count`

`set listsize unlimited`

Make the `list` command display `count` to `unlimited` or 0 means there's no limit.

`show listsize`

Display the number of lines that `list` prints.

Repeating a `list` command with RET discards the argument, so it is equivalent to typing just `list`. This is more useful than listing the same lines again. An exception is made for an argument of '`-`'; that argument is preserved in repetition so that each repetition moves up in the source file.

In general, the `list` command expects you to supply zero, one or two location specs. These location specs are interpreted to resolve to source code lines; there are several ways of writing them (see [Location Specifications](Location-Specifications.html#Location-Specifications)), but the effect is always to resolve to some source lines to display.

Here is a complete description of the possible arguments for `list`:

`list locspec`

:   Print lines centered around the line or lines of all the code locations that result from resolving `locspec`.

`list first,last`

:   Print lines from `first` resolve to more than one source line in the program, then the list command shows the list of resolved source lines and does not proceed with the source code listing.

`list ,last`

:   Print lines ending with `last`.

```
Likewise, if `last` resolves to more than one source line in the program, then the list command prints the list of resolved source lines and does not proceed with the source code listing.
```

`list first,`

:   Print lines starting with `first`.

`list +`

:   Print lines just after the lines last printed.

`list -`

:   Print lines just before the lines last printed.

`list`

:   As described in the preceding table.

---

::: header
Next: [Location Specifications](Location-Specifications.html#Location-Specifications)]
:::
