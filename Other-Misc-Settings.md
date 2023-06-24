---
tip: translate by openai@2023-06-24 00:50:08
...
---
description: Other Misc Settings (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Other Misc Settings (Debugging with GDB)
lang: en
resource-type: document
title: Other Misc Settings (Debugging with GDB)
---
::: header
Previous: [Debugging Output](Debugging-Output.html#Debugging-Output)]
:::

---

### 22.11 Other Miscellaneous Settings

`set interactive-mode`


If `on`, forces [GDB] tries to determine whether its standard input is a terminal, and works in interactive-mode if it is, non-interactively otherwise.

> 如果设置为“on”，[GDB] 将尝试确定其标准输入是否为终端，如果是，则以交互模式工作，否则以非交互模式工作。


In the vast majority of cases, the debugger should be able to guess correctly which mode should be used. But this setting can be useful in certain specific cases, such as running a MinGW [GDB] inside a cygwin window.

> 在绝大多数情况下，调试器应该能够正确猜测应该使用哪种模式。但是在某些特定的情况下，比如在cygwin窗口中运行MinGW [GDB]，这个设置是有用的。

`show interactive-mode`

Displays whether the debugger is operating in interactive mode or not.

`set suppress-cli-notifications`


If `on`, command-line-interface (CLI) notifications that are printed by [GDB] are suppressed. If `off`, the notifications are printed as usual. The default value is `off`. CLI notifications occur when you change the selected context or when the program being debugged stops, as detailed below.

> 如果设置为“on”，[GDB]打印的命令行界面（CLI）通知将被抑制。如果设置为“off”，通知将正常打印。默认值为“off”。当您更改所选上下文或被调试程序停止时，会发生CLI通知，如下所述。

*User-selected context changes:*


:   When you change the selected context (i.e. the current inferior, thread and/or the frame), [GDB] prints information about the new context. For example, the default behavior is below:

> 当您更改所选上下文（即当前下级、线程和/或帧）时，[GDB]会打印有关新上下文的信息。例如，默认行为如下：

```
::: smallexample
``` smallexample
(gdb) inferior 1
[Switching to inferior 1 [process 634] (/tmp/test)]
[Switching to thread 1 (process 634)]
#0  main () at test.c:3
3         return 0;
(gdb)
```

:::

When the notifications are suppressed, the new context is not printed:

::: smallexample

```bash
(gdb) set suppress-cli-notifications on
(gdb) inferior 1
(gdb)
```

:::

```

*The program being debugged stops:*


:   When the program you are debugging stops (e.g. because of hitting a breakpoint, completing source-stepping, an interrupt, etc.), [GDB] prints information about the stop event. For example, below is a breakpoint hit:

> 当你正在调试的程序停止（例如因为遇到断点、完成源代码跟踪、中断等），[GDB]会打印出有关停止事件的信息。例如，下面是一个断点触发：

```

::: smallexample

```bash
(gdb) break test.c:3
Breakpoint 2 at 0x555555555155: file test.c, line 3.
(gdb) continue
Continuing.

Breakpoint 2, main () at test.c:3
3         return 0;
(gdb)
```

:::

When the notifications are suppressed, the output becomes:

::: smallexample

```bash
(gdb) break test.c:3
Breakpoint 2 at 0x555555555155: file test.c, line 3.
(gdb) set suppress-cli-notifications on
(gdb) continue
Continuing.
(gdb)
```

:::

Suppressing CLI notifications may be useful in scripts to obtain a reduced output from a list of commands.

```



`show suppress-cli-notifications`

Displays whether printing CLI notifications is suppressed or not.

---

::: header
Previous: [Debugging Output](Debugging-Output.html#Debugging-Output)]
:::
```
