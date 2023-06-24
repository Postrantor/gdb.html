---
tip: translate by openai@2023-06-23 20:07:38
...
---
description: CRIS (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: CRIS (Debugging with GDB)
lang: en
resource-type: document
title: CRIS (Debugging with GDB)
---
::: header
Next: [Super-H](Super_002dH.html#Super_002dH)]
:::

---

#### 21.3.10 CRIS


When configured for debugging CRIS, [GDB] provides the following CRIS-specific commands:

> 当配置用于调试CRIS时，[GDB]提供以下专门针对CRIS的命令：

`set cris-version ver`

:

```
Set the current CRIS version to `ver`'. The CRIS version affects register names and sizes. This command is useful in case autodetection of the CRIS version fails.
```

`show cris-version`

:   Show the current CRIS version.

`set cris-dwarf2-cfi`

:

```
Set the usage of DWARF-2 CFI for CRIS debugging. The default is '`on`' when using `gcc-cris` whose version is below `R59`.
```

`show cris-dwarf2-cfi`

:   Show the current state of using DWARF-2 CFI.

`set cris-mode mode`

:

```
Set the current CRIS mode to `mode`').
```

`show cris-mode`

:   Show the current CRIS mode.
