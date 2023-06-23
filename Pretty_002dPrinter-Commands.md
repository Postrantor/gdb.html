---
description: Pretty-Printer Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Pretty-Printer Commands (Debugging with GDB)
lang: en
resource-type: document
title: Pretty-Printer Commands (Debugging with GDB)
---
::: header
Previous: [Pretty-Printer Example](Pretty_002dPrinter-Example.html#Pretty_002dPrinter-Example)]
:::

---

#### 10.10.3 Pretty-Printer Commands

`info pretty-printer [object-regexp [name-regexp]]`

Print the list of installed pretty-printers. This includes disabled pretty-printers, which are marked as such.

`object-regexp` looks up a printer from these three objects.

`name-regexp` is a regular expression matching the name of the printers to list.

`disable pretty-printer [object-regexp [name-regexp]]`

Disable pretty-printers matching `object-regexp`. A disabled pretty-printer is not forgotten, it may be enabled again later.

`enable pretty-printer [object-regexp [name-regexp]]`

Enable pretty-printers matching `object-regexp`.

Example:

Suppose we have three pretty-printers installed: one from library1.so named `foo` that prints objects of type `foo`, and another from library2.so named `bar` that prints two types of objects, `bar1` and `bar2`.

::: smallexample

```bash
(gdb) info pretty-printer
library1.so:
  foo
library2.so:
  bar
    bar1
    bar2
```

```bash
(gdb) info pretty-printer library2
library2.so:
  bar
    bar1
    bar2
```

```bash
(gdb) disable pretty-printer library1
1 printer disabled
2 of 3 printers enabled
(gdb) info pretty-printer
library1.so:
  foo [disabled]
library2.so:
  bar
    bar1
    bar2
```

```bash
(gdb) disable pretty-printer library2 bar;bar1
1 printer disabled
1 of 3 printers enabled
(gdb) info pretty-printer library2
library2.so:
  bar
    bar1 [disabled]
    bar2
```

```bash
(gdb) disable pretty-printer library2 bar
1 printer disabled
0 of 3 printers enabled
(gdb) info pretty-printer
library1.so:
  foo [disabled]
library2.so:
  bar [disabled]
    bar1 [disabled]
    bar2
```

:::

Note that for `bar` the entire printer can be disabled, as can each individual subprinter.

Printing values and frame arguments is done by default using the enabled pretty printers.

The print option `-raw-values` and [GDB] setting `set print raw-values` (see [set print raw-values](Print-Settings.html#set-print-raw_002dvalues)) can be used to print values without applying the enabled pretty printers.

Similarly, the backtrace option `-raw-frame-arguments` and [GDB] setting `set print raw-frame-arguments` (see [set print raw-frame-arguments](Print-Settings.html#set-print-raw_002dframe_002darguments)) can be used to ignore the enabled pretty printers when printing frame argument values.

---

::: header
Previous: [Pretty-Printer Example](Pretty_002dPrinter-Example.html#Pretty_002dPrinter-Example)]
:::
