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

In the vast majority of cases, the debugger should be able to guess correctly which mode should be used. But this setting can be useful in certain specific cases, such as running a MinGW [GDB] inside a cygwin window.

`show interactive-mode`

Displays whether the debugger is operating in interactive mode or not.

`set suppress-cli-notifications`

If `on`, command-line-interface (CLI) notifications that are printed by [GDB] are suppressed. If `off`, the notifications are printed as usual. The default value is `off`. CLI notifications occur when you change the selected context or when the program being debugged stops, as detailed below.

*User-selected context changes:*

:   When you change the selected context (i.e. the current inferior, thread and/or the frame), [GDB] prints information about the new context. For example, the default behavior is below:

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
