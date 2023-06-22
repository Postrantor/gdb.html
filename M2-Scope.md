---
description: M2 Scope (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: M2 Scope (Debugging with GDB)
lang: en
resource-type: document
title: M2 Scope (Debugging with GDB)
---
::: header
Next: [GDB/M2](GDB_002fM2.html#GDB_002fM2)]
:::

---

#### 15.4.9.8 The Scope Operators `::` and `.`

There are a few subtle differences between the Modula-2 scope operator (`.`) and the [GDB] scope operator (`::`). The two have similar syntax:

::: smallexample

```bash
module . id
scope :: id
```

:::

where `scope` is any declared identifier within your program, except another module.

Using the `::` operator makes [GDB].

Using the `.` operator makes [GDB].
