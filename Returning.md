---
tip: translate by openai@2023-06-24 02:10:47
...
---
description: Returning (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Returning (Debugging with GDB)
lang: en
resource-type: document
title: Returning (Debugging with GDB)
---
::: header
Next: [Calling](Calling.html#Calling)]
:::

---

### 17.4 Returning from a Function

`return`

`return expression`


You can cancel execution of a function call with the `return` command. If you give an `expression` argument, its value is used as the function's return value.

> 你可以使用`return`命令取消函数调用的执行。如果给出一个`表达式`参数，它的值将被用作函数的返回值。


When you use `return`, [GDB] discards the selected stack frame (and all frames within it). You can think of this as making the discarded frame return prematurely. If you wish to specify a value to be returned, give that value as the argument to `return`.

> 当你使用`return`时，[GDB]会放弃选定的堆栈帧（以及其中的所有帧）。你可以把它想象成使被放弃的帧提前返回。如果你想指定一个要返回的值，请将该值作为`return`的参数。


This pops the selected stack frame (see [Selecting a Frame](Selection.html#Selection)), and any other frames inside of it, leaving its caller as the innermost remaining frame. That frame becomes selected. The specified value is stored in the registers used for returning values of functions.

> 这会弹出所选择的堆栈帧（参见[选择帧](Selection.html#Selection)），以及它内部的其他帧，使其调用者成为最内部的剩余帧。该帧将被选中。指定的值将存储在用于函数返回值的寄存器中。


The `return` command does not resume execution; it leaves the program stopped in the state that would exist if the function had just returned. In contrast, the `finish` command (see [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping)) resumes execution until the selected stack frame returns naturally.

> 命令`return`不会恢复执行；它会使程序停留在函数刚刚返回时的状态。相比之下，命令`finish`（参见[继续和步进](Continuing-and-Stepping.html#Continuing-and-Stepping)）会恢复执行，直到所选择的堆栈帧自然返回。


[GDB] already knows the OS ABI from its current target so it needs to find out also the type being returned to make the assignment into the right register(s).

> GDB已经从当前目标中了解操作系统ABI，因此它还需要找出要分配到正确寄存器的返回类型。


Normally, the selected stack frame has debug info. [GDB] transparently converts the implicit `int` value of -1 into a `long long int`:

> 一般来说，选定的堆栈帧具有调试信息。[GDB]会透明地将-1的隐式`int`值转换为`long long int`：

::: smallexample

```bash
Breakpoint 1, func () at gdb.base/return-nodebug.c:29
29        return 31;
(gdb) return -1
Make func return now? (y or n) y
#0  0x004004f6 in main () at gdb.base/return-nodebug.c:43
43        printf ("result=%lld\n", func ());
(gdb)
```

:::


However, if the selected stack frame does not have a debug info, e.g., if the function was compiled without debug info, [GDB] with its implicit type `int` would set only a part of a `long long int` result for a debug info less function (on 32-bit architectures). Therefore the user is required to specify the return type by an appropriate cast explicitly:

> 然而，如果所选的堆栈帧没有调试信息，例如函数是没有调试信息编译的，[GDB]会使用其隐式类型`int`来设置调试信息较少的函数（在32位架构上）的`long long int`结果的一部分。因此，用户需要通过适当的转换显式指定返回类型：

::: smallexample

```bash
Breakpoint 2, 0x0040050b in func ()
(gdb) return -1
Return value type not available for selected stack frame.
Please use an explicit cast of the value to return.
(gdb) return (long long int) -1
Make selected stack frame return now? (y or n) y
#0  0x00400526 in main ()
(gdb)
```

:::

---

::: header
Next: [Calling](Calling.html#Calling)]
:::
