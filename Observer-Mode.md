---
tip: translate by openai@2023-06-24 00:42:21
...
---
description: Observer Mode (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Observer Mode (Debugging with GDB)
lang: en
resource-type: document
title: Observer Mode (Debugging with GDB)
---
::: header
Previous: [Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls)]
:::

---

#### 5.5.6 Observer Mode


If you want to build on non-stop mode and observe program behavior without any chance of disruption by [GDB], you can set variables to disable all of the debugger's attempts to modify state, whether by writing memory, inserting breakpoints, etc. These operate at a low level, intercepting operations from all commands.

> 如果你想要连续构建，并观察程序行为，而不受[GDB]中断的影响，你可以设置变量来禁用调试器尝试修改状态的所有操作，无论是写入内存，插入断点等。这些操作都是在低级别上进行的，拦截所有命令的操作。


When all of these are set to `off`, then [GDB] is said to be *observer mode*. As a convenience, the variable `observer` can be set to disable these, plus enable non-stop mode.

> 当这些都设置为“关闭”时，GDB就被称为“观察者模式”。为了方便起见，可以将变量“observer”设置为关闭这些，并启用非停止模式。


Note that [GDB] will not prevent you from making nonsensical combinations of these settings. For instance, if you have enabled `may-insert-breakpoints` but disabled `may-write-memory`, then breakpoints that work by writing trap instructions into the code stream will still not be able to be placed.

> 注意，GDB不会阻止您使用这些设置进行无意义的组合。例如，如果您已经启用了“may-insert-breakpoints”，但禁用了“may-write-memory”，那么通过将陷阱指令写入代码流来工作的断点仍然无法设置。

`set observer on`

`set observer off`


When set to `on`, this disables all the permission variables below (except for `insert-fast-tracepoints`), plus enables non-stop debugging. Setting this to `off` switches back to normal debugging, though remaining in non-stop mode.

> 当设置为“开”时，这将禁用下面的所有权限变量（除“插入快速跟踪点”外），并启用非停止调试。将此设置更改为“关”时，将切换回正常调试，但仍保持在非停止模式下。

`show observer`

Show whether observer mode is on or off.

`set may-write-registers on`

`set may-write-registers off`


This controls whether [GDB] will attempt to alter the values of registers, such as with assignment expressions in `print`, or the `jump` command. It defaults to `on`.

> 这控制GDB是否尝试改变寄存器的值，比如使用`print`中的赋值表达式或`jump`命令。它的默认值为“开”。

`show may-write-registers`

Show the current permission to write registers.

`set may-write-memory on`

`set may-write-memory off`


This controls whether [GDB] will attempt to alter the contents of memory, such as with assignment expressions in `print`. It defaults to `on`.

> 这控制了[GDB]是否会尝试改变内存的内容，比如使用`print`中的赋值表达式。默认设置为`开启`。

`show may-write-memory`

Show the current permission to write memory.

`set may-insert-breakpoints on`

`set may-insert-breakpoints off`

This controls whether [GDB]. It defaults to `on`.

`show may-insert-breakpoints`

Show the current permission to insert breakpoints.

`set may-insert-tracepoints on`

`set may-insert-tracepoints off`


This controls whether [GDB] will attempt to insert (regular) tracepoints at the beginning of a tracing experiment. It affects only non-fast tracepoints, fast tracepoints being under the control of `may-insert-fast-tracepoints`. It defaults to `on`.

> 这控制GDB是否会在跟踪实验开始时尝试插入（常规）跟踪点。它仅影响非快速跟踪点，快速跟踪点受`may-insert-fast-tracepoints`控制。默认为“开启”。

`show may-insert-tracepoints`

Show the current permission to insert tracepoints.

`set may-insert-fast-tracepoints on`

`set may-insert-fast-tracepoints off`


This controls whether [GDB] will attempt to insert fast tracepoints at the beginning of a tracing experiment. It affects only fast tracepoints, regular (non-fast) tracepoints being under the control of `may-insert-tracepoints`. It defaults to `on`.

> 这控制GDB是否尝试在跟踪实验开始时插入快速跟踪点。它仅影响快速跟踪点，常规（非快速）跟踪点由`may-insert-tracepoints`控制。它的默认值为`on`。

`show may-insert-fast-tracepoints`

Show the current permission to insert fast tracepoints.

`set may-interrupt on`

`set may-interrupt off`

This controls whether [GDB]. It defaults to `on`.

`show may-interrupt`

Show the current permission to interrupt or stop the program.

---

::: header
Previous: [Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls)]
:::
