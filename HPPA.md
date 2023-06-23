---
description: HPPA (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: HPPA (Debugging with GDB)
lang: en
resource-type: document
title: HPPA (Debugging with GDB)
---
::: header
Next: [PowerPC](PowerPC.html#PowerPC)]
:::

---

#### 21.4.5 HPPA

When [GDB] is debugging the HP PA architecture, it provides the following special commands:

`set debug hppa`

:

```
This command determines whether HPPA architecture-specific debugging messages are to be displayed.
```

`show debug hppa`

:   Show whether HPPA debugging messages are displayed.

`maint print unwind address`

:

```
This command displays the contents of the unwind table entry at the given `address`.
```
