---
tip: translate by openai@2023-06-24 01:10:03
...
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

> 打印已安装的漂亮打印机列表。其中包括已禁用的漂亮打印机，它们会被标记出来。

`object-regexp` looks up a printer from these three objects.

`name-regexp` is a regular expression matching the name of the printers to list.

`disable pretty-printer [object-regexp [name-regexp]]`


Disable pretty-printers matching `object-regexp`. A disabled pretty-printer is not forgotten, it may be enabled again later.

> 禁用与`object-regexp`匹配的美化打印机。禁用的美化打印机不会被遗忘，以后可以再次启用。

`enable pretty-printer [object-regexp [name-regexp]]`

Enable pretty-printers matching `object-regexp`.

Example:


Suppose we have three pretty-printers installed: one from library1.so named `foo` that prints objects of type `foo`, and another from library2.so named `bar` that prints two types of objects, `bar1` and `bar2`.

> 假设我们安装了三个漂亮的打印机：一个来自library1.so，名为“foo”，可以打印类型为“foo”的对象，另一个来自library2.so，名为“bar”，可以打印两种类型的对象，即“bar1”和“bar2”。

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

> 注意，对于`bar`，整个打印机可以被禁用，每个单独的子打印机也可以被禁用。


Printing values and frame arguments is done by default using the enabled pretty printers.

> 默认情况下，使用启用的漂亮打印机来打印值和框架参数。


The print option `-raw-values` and [GDB] setting `set print raw-values` (see [set print raw-values](Print-Settings.html#set-print-raw_002dvalues)) can be used to print values without applying the enabled pretty printers.

> 打印选项`-raw-values`和[GDB]设置`set print raw-values`（参见[set print raw-values](Print-Settings.html#set-print-raw_002dvalues)）可用于在不应用启用的美化打印机的情况下打印值。


Similarly, the backtrace option `-raw-frame-arguments` and [GDB] setting `set print raw-frame-arguments` (see [set print raw-frame-arguments](Print-Settings.html#set-print-raw_002dframe_002darguments)) can be used to ignore the enabled pretty printers when printing frame argument values.

> 同样，可以使用回溯选项`-raw-frame-arguments`和[GDB]设置`set print raw-frame-arguments`（参见[set print raw-frame-arguments](Print-Settings.html#set-print-raw_002dframe_002darguments)）来忽略启用的漂亮的打印机，以便打印帧参数值。

---

::: header
Previous: [Pretty-Printer Example](Pretty_002dPrinter-Example.html#Pretty_002dPrinter-Example)]
:::
