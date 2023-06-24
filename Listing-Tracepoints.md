---
tip: translate by openai@2023-06-24 10:24:17
...
---
description: Listing Tracepoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Listing Tracepoints (Debugging with GDB)
lang: en
resource-type: document
title: Listing Tracepoints (Debugging with GDB)
---
::: header
Next: [Listing Static Tracepoint Markers](Listing-Static-Tracepoint-Markers.html#Listing-Static-Tracepoint-Markers)]
:::

---

#### 13.1.7 Listing Tracepoints

`info tracepoints [num…]`


Display information about the tracepoint `num`. If you don't specify a tracepoint number, displays information about all the tracepoints defined so far. The format is similar to that used for `info breakpoints`; in fact, `info tracepoints` is the same command, simply restricting itself to tracepoints.

> 顯示有關斷點`num`的信息。如果您沒有指定斷點號，則會顯示有關目前定義的所有斷點的信息。格式類似於`info breakpoints`; 事實上，`info tracepoints`是相同的命令，只是僅限斷點。


A tracepoint's listing may include additional information specific to tracing:

> 跟踪点的列表可能包括与跟踪相关的附加信息。

- its passcount as given by the `passcount n` command
- the state about installed on target of each location

::: smallexample

```bash
(gdb) info trace
Num     Type           Disp Enb Address    What
1       tracepoint     keep y   0x0804ab57 in foo() at main.cxx:7
        while-stepping 20
          collect globfoo, $regs
        end
        collect globfoo2
        end
        pass count 1200 
2       tracepoint     keep y   <MULTIPLE>
        collect $eip
2.1                         y     0x0804859c in func4 at change-loc.h:35
        installed on target
2.2                         y     0xb7ffc480 in func4 at change-loc.h:35
        installed on target
2.3                         y     <PENDING>  set_tracepoint
3       tracepoint     keep y   0x080485b1 in foo at change-loc.c:29
        not installed on target
(gdb)
```

:::

This command can be abbreviated `info tp`.
