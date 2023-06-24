---
tip: translate by openai@2023-06-23 16:57:09
...
---
description: Ada Exceptions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Exceptions (Debugging with GDB)
lang: en
resource-type: document
title: Ada Exceptions (Debugging with GDB)
------------------------------------------

::: header
Next: [Ada Tasks](Ada-Tasks.html#Ada-Tasks)]
:::

---

#### 15.4.10.6 Ada Exceptions

A command is provided to list all Ada exceptions:

> 提供了一个命令来列出所有 Ada 异常：

`info exceptions`

`info exceptions regexp`

The `info exceptions` command allows you to list all Ada exceptions defined within the program being debugged, as well as their addresses. With a regular expression, `regexp` are listed.

> `info exceptions` 命令允许您列出在被调试的程序中定义的所有 Ada 异常，以及它们的地址。 使用正则表达式，`regexp` 将被列出。

Below is a small example, showing how the command can be used, first without argument, and next with a regular expression passed as an argument.

> 下面是一个小例子，展示了如何使用该命令，先不带参数，然后传递一个正则表达式作为参数。

::: smallexample

```bash
(gdb) info exceptions
All defined Ada exceptions:
constraint_error: 0x613da0
program_error: 0x613d20
storage_error: 0x613ce0
tasking_error: 0x613ca0
const.aint_global_e: 0x613b00
(gdb) info exceptions const.aint
All Ada exceptions matching regular expression "const.aint":
constraint_error: 0x613da0
const.aint_global_e: 0x613b00
```

:::

It is also possible to ask [GDB] to stop your program's execution when an exception is raised. For more details, see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints).

> 可以向 GDB 请求，当异常被触发时停止程序的执行。更多细节，请参阅[设置捕获点](Set-Catchpoints.html#Set-Catchpoints)。
