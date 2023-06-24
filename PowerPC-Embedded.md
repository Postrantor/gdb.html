---
tip: translate by openai@2023-06-24 01:06:09
...
---
description: PowerPC Embedded (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: PowerPC Embedded (Debugging with GDB)
lang: en
resource-type: document
title: PowerPC Embedded (Debugging with GDB)
---
::: header
Next: [AVR](AVR.html#AVR)]
:::

---

#### 21.3.8 PowerPC Embedded


[GDB] supports using the DVC (Data Value Compare) register to implement in hardware simple hardware watchpoint conditions of the form:

> [GDB] 支持使用 DVC (数据值比较) 寄存器来实现简单的硬件监视点条件，形式如：

::: smallexample

```bash
(gdb) watch address|variable \
  if  address|variable == constant expression
```

:::


The DVC register will be automatically used when [GDB] running on a Linux kernel version 2.6.34 or newer.

> DVC登记将在运行Linux内核版本2.6.34或更新版本的GDB时自动使用。


When running on PowerPC embedded processors, [GDB] automatically uses ranged hardware watchpoints, unless the `exact-watchpoints` option is on, in which case watchpoints using only one debug register are created when watching variables of scalar types.

> 当在PowerPC嵌入式处理器上运行时，GDB会自动使用范围硬件断点，除非`exact-watchpoints`选项开启，在这种情况下，当监视标量类型的变量时，将使用单个调试寄存器创建断点。


You can create an artificial array to watch an arbitrary memory region using one of the following commands (see [Expressions](Expressions.html#Expressions)):

> 你可以使用以下命令之一来创建一个人工数组以观察任意的内存区域（请参阅[表达式](Expressions.html#Expressions)）：

::: smallexample

```bash
(gdb) watch *((char *) address)@length
(gdb) watch  address
```

:::


PowerPC embedded processors support masked watchpoints. See the discussion about the `mask` argument in [Set Watchpoints](Set-Watchpoints.html#Set-Watchpoints).

> 功耗PC嵌入式处理器支持蒙版式断点。参见[设置断点](Set-Watchpoints.html#Set-Watchpoints)中关于`mask`参数的讨论。


PowerPC embedded processors support hardware accelerated *ranged breakpoints*. A ranged breakpoint stops execution of the inferior whenever it executes an instruction at any address within the range it was set at. To set a ranged breakpoint in [GDB], use the `break-range` command.

> PowerPC嵌入式处理器支持硬件加速的范围断点。范围断点可以在设置范围内的任何地址执行指令时停止下级执行。要在[GDB]中设置范围断点，请使用“break-range”命令。

[GDB] provides the following PowerPC-specific commands:

`break-range start-locspec, end-locspec`


Set a breakpoint for an address range given by `start-locspec` resolve to multiple code locations in the program, then the command aborts with an error without creating a breakpoint.

> 当给定的start-locspec解析为程序中的多个代码位置时，命令会在没有创建断点的情况下中止并发出错误。

`set powerpc soft-float`

`show powerpc soft-float`


Force [GDB] selects the calling convention based on the selected architecture and the provided executable file.

> GDB根据选择的架构和提供的可执行文件选择调用约定。

`set powerpc vector-abi`

`show powerpc vector-abi`


Force [GDB] selects the calling convention based on the selected architecture and the provided executable file.

> 力[GDB]根据所选择的架构和提供的可执行文件来选择调用约定。

`set powerpc exact-watchpoints`

`show powerpc exact-watchpoints`


Allow [GDB] to use only one debug register when watching a variable of scalar type, thus assuming that the variable is accessed through the address of its first byte.

> 允许GDB在监视标量类型的变量时只使用一个调试寄存器，假设该变量是通过其第一个字节的地址访问的。

---

::: header
Next: [AVR](AVR.html#AVR)]
:::
