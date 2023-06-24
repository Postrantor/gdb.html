---
tip: translate by openai@2023-06-24 03:25:53
...
---
description: Super-H (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Super-H (Debugging with GDB)
lang: en
resource-type: document
title: Super-H (Debugging with GDB)
---
::: header
Previous: [CRIS](CRIS.html#CRIS)]
:::

---

#### 21.3.11 Renesas Super-H

For the Renesas Super-H processor, [GDB] provides these commands:

`set sh calling-convention convention`

:

```
Set the calling-convention used when calling functions from [GDB]' if debug information is missing, or the compiler does not emit the DWARF-2 calling convention entry for a function.
```

`show sh calling-convention`

:

```
Show the current calling convention setting.
```
