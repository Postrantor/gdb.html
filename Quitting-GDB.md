---
description: Quitting GDB (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Quitting GDB (Debugging with GDB)
lang: en
resource-type: document
title: Quitting GDB (Debugging with GDB)
---
::: header
Next: [Shell Commands](Shell-Commands.html#Shell-Commands)]
:::

---

### 2.2 Quitting [GDB]

`quit [expression]`

`exit [expression]`

`q`

To exit [GDB] as the error code.

An interrupt (often [Ctrl-c] does not allow it to take effect until a time when it is safe.

If you have been using [GDB] to control an attached process or device, you can release it with the `detach` command (see [Debugging an Already-running Process](Attach.html#Attach)).
