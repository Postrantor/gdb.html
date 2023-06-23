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

`-a`

:   Dump all memory mappings. The actual effect of this option depends on the Operating System. On [GNU]/Linux, it will disable `use-coredump-filter` (see [set use-coredump-filter](Core-File-Generation.html#set-use_002dcoredump_002dfilter)) and enable `dump-excluded-mappings` (see [set dump-excluded-mappings](Core-File-Generation.html#set-dump_002dexcluded_002dmappings)).

`-o prefix`

:   The optional argument `prefix`.
