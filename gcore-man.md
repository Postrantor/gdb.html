---
tip: translate by openai@2023-06-23 21:32:20
...
---
description: gcore man (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: gcore man (Debugging with GDB)
lang: en
resource-type: document
title: gcore man (Debugging with GDB)
---
::: header
Next: [gdbinit man](gdbinit-man.html#gdbinit-man)]
:::

---

#### gcore man

### gcore

::: format

```format
gcore [-a] [-o prefix] pid1 [pid2...pidN]
```

:::


Generate core dumps of one or more running programs with process IDs `pid1` was used to set up an appropriate core dump limit). However, unlike after a crash, after `gcore` finishes its job the program remains running without any change.

> 生成一个或多个正在运行的程序的核心转储，使用进程ID `pid1`来设置适当的核心转储限制。但是，与崩溃后不同，`gcore`完成其工作后，程序仍在运行而没有任何改变。

`-a`


:   Dump all memory mappings. The actual effect of this option depends on the Operating System. On [GNU]/Linux, it will disable `use-coredump-filter` (see [set use-coredump-filter](Core-File-Generation.html#set-use_002dcoredump_002dfilter)) and enable `dump-excluded-mappings` (see [set dump-excluded-mappings](Core-File-Generation.html#set-dump_002dexcluded_002dmappings)).

> 导出所有内存映射。此选项的实际效果取决于操作系统。在[GNU]/Linux上，它将禁用`use-coredump-filter`（参见[设置use-coredump-filter]（Core-File-Generation.html#set-use_002dcoredump_002dfilter））并启用`dump-excluded-mappings`（参见[设置dump-excluded-mappings]（Core-File-Generation.html#set-dump_002dexcluded_002dmappings））。

`-o prefix`

:   The optional argument `prefix`.
