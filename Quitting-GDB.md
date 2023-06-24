---
tip: translate by openai@2023-06-24 01:44:59
...
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

> 一个中断（通常是[Ctrl-c]）不会在安全的时候生效。


If you have been using [GDB] to control an attached process or device, you can release it with the `detach` command (see [Debugging an Already-running Process](Attach.html#Attach)).

> 如果您一直使用GDB来控制一个附加的进程或设备，您可以使用`detach`命令来释放它（参见[调试已经运行的进程](Attach.html#Attach)）。
