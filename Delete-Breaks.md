---
description: Delete Breaks (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Delete Breaks (Debugging with GDB)
lang: en
resource-type: document
title: Delete Breaks (Debugging with GDB)
---
::: header
Next: [Disabling](Disabling.html#Disabling)]
:::

---

#### 5.1.4 Deleting Breakpoints

It is often necessary to eliminate a breakpoint, watchpoint, or catchpoint once it has done its job and you no longer want your program to stop there. This is called *deleting* the breakpoint. A breakpoint that has been deleted no longer exists; it is forgotten.

With the `clear` command you can delete breakpoints according to where they are in your program. With the `delete` command you can delete individual breakpoints, watchpoints, or catchpoints by specifying their breakpoint numbers.

It is not necessary to delete a breakpoint to proceed past it. [GDB] automatically ignores breakpoints on the first instruction to be executed when you continue execution without changing the execution address.

`clear`

Delete any breakpoints at the next instruction to be executed in the selected stack frame (see [Selecting a Frame](Selection.html#Selection)). When the innermost frame is selected, this is a good way to delete a breakpoint where your program just stopped.

`clear locspec`

Delete any breakpoint with a code location that corresponds to `locspec`:

`linenum`
`filename:linenum`
`-line linenum`
`-source filename -line linenum`

:   If `locspec` is omitted, it defaults to the current source file.

`*address`

:   If `locspec`.

`function`
`-function function`

:   If `locspec`.

Ambiguity in names of files and functions can be resolved as described in [Location Specifications](Location-Specifications.html#Location-Specifications).

`delete [breakpoints] [list…]`

Delete the breakpoints, watchpoints, or catchpoints of the breakpoint list specified as argument. If no argument is specified, delete all breakpoints ([GDB] asks confirmation, unless you have `set confirm off`). You can abbreviate this command as `d`.

---

::: header
Next: [Disabling](Disabling.html#Disabling)]
:::
