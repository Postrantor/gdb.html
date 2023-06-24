---
tip: translate by openai@2023-06-24 00:56:07
...
---
description: Overlay Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Overlay Commands (Debugging with GDB)
lang: en
resource-type: document
title: Overlay Commands (Debugging with GDB)
---
::: header
Next: [Automatic Overlay Debugging](Automatic-Overlay-Debugging.html#Automatic-Overlay-Debugging)]
:::

---

### 14.2 Overlay Commands


To use [GDB] to determine the appropriate address of a function or variable, depending on whether the overlay is mapped or not.

> 使用GDB来确定函数或变量的适当地址，取决于是否已映射覆盖。


[GDB]'s overlay commands all start with the word `overlay`; you can abbreviate this as `ov` or `ovly`. The commands are:

> `GDB` 的覆盖命令都以“覆盖”（overlay）这个词开头；你可以简写为`ov`或`ovly`。这些命令是：

`overlay off`

:

```
Disable [GDB]'s overlay support is disabled.
```

`overlay manual`

:

```
Enable *manual* overlay debugging. In this mode, [GDB] relies on you to tell it which overlays are mapped, and which are not, using the `overlay map-overlay` and `overlay unmap-overlay` commands described below.
```

`overlay map-overlay overlay`
`overlay map overlay`

:

```
Tell [GDB] are now unmapped.
```

`overlay unmap-overlay overlay`
`overlay unmap overlay`

:

```
Tell [GDB] assumes it can find the overlay's functions and variables at their load addresses.
```

`overlay auto`


:   Enable *automatic* overlay debugging. In this mode, [GDB] consults a data structure the overlay manager maintains in the inferior to see which overlays are mapped. For details, see [Automatic Overlay Debugging](Automatic-Overlay-Debugging.html#Automatic-Overlay-Debugging).

> 启用*自动*覆盖调试。在此模式下，[GDB]查询下位机维护的覆盖管理器维护的数据结构，以查看哪些覆盖被映射。有关详细信息，请参阅[Automatic Overlay Debugging](Automatic-Overlay-Debugging.html#Automatic-Overlay-Debugging)。

`overlay load-target`
`overlay load`

:

```
Re-read the overlay table from the inferior. Normally, [GDB]. This command is only useful when using automatic overlay debugging.
```

`overlay list-overlays`
`overlay list`

:

```
Display a list of the overlays currently mapped, along with their mapped addresses, load addresses, and sizes.
```


Normally, when [GDB] prints a code address, it includes the name of the function the address falls in:

> 通常，当[GDB]打印一个代码地址时，它会包括该地址所属函数的名称：

::: smallexample

```bash
(gdb) print main
$3 =  0x11a0 <main>
```

:::

When overlay debugging is enabled, [GDB] prints it this way:

::: smallexample

```bash
(gdb) overlay list
No sections are mapped.
(gdb) print foo
$5 =  0x100000 <*foo*>
```

:::


When `foo`'s overlay is mapped, [GDB] prints the function's name normally:

> 当`foo`的覆盖被映射时，[GDB]会正常打印出函数的名称：

::: smallexample

```bash
(gdb) overlay list
Section .ov.foo.text, loaded at 0x100000 - 0x100034,
        mapped at 0x1016 - 0x104a
(gdb) print foo
$6 =  0x1016 <foo>
```

:::


When overlay debugging is enabled, [GDB]'s breakpoint support has some limitations:

> 当启用覆盖调试时，GDB的断点支持有一些局限性：

- can write to the overlay at its load address.
- [GDB] will re-set its breakpoints properly.

---

::: header
Next: [Automatic Overlay Debugging](Automatic-Overlay-Debugging.html#Automatic-Overlay-Debugging)]
:::
