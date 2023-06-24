---
tip: translate by openai@2023-06-23 23:45:10
...
---
description: Jumping (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Jumping (Debugging with GDB)
lang: en
resource-type: document
title: Jumping (Debugging with GDB)
---
::: header
Next: [Signaling](Signaling.html#Signaling)]
:::

---

### 17.2 Continuing at a Different Address


Ordinarily, when you continue your program, you do so at the place where it stopped, with the `continue` command. You can instead continue at an address of your own choosing, with the following commands:

> 一般来说，当你继续你的程序时，你可以使用`continue`命令从上次停止的地方继续。你也可以选择自己想去的地址，使用以下命令：

`jump locspec`

`j locspec`


Resume execution at the address of the code location that results from resolving `locspec` resolves to more than one address, those outside the current compilation unit are ignored. If considering just the addresses in the current compilation unit still doesn't yield a unique address, the command aborts before jumping. Execution stops again immediately if there is a breakpoint there. It is common practice to use the `tbreak` command in conjunction with `jump`. See [Setting Breakpoints](Set-Breaks.html#Set-Breaks).

> 恢复执行位置是由`locspec`解析出来的代码位置，如果解析出来的地址不止一个，则会忽略那些位于当前编译单元之外的地址。如果只考虑当前编译单元中的地址仍然不能产生唯一的地址，该命令将在跳转之前中止。如果那里有断点，执行将会立即停止。通常情况下，会使用`tbreak`命令与`jump`命令结合使用，参见[设置断点](Set-Breaks.html#Set-Breaks)。


The `jump` command does not change the current stack frame, or the stack pointer, or the contents of any memory location or any register other than the program counter. If `locspec` resolves to an address in a different function from the one currently executing, the results may be bizarre if the two functions expect different patterns of arguments or of local variables. For this reason, the `jump` command requests confirmation if the jump address is not in the function currently executing. However, even bizarre results are predictable if you are well acquainted with the machine-language code of your program.

> 跳转命令不会改变当前的堆栈帧，堆栈指针，内存位置的内容或者任何除了程序计数器以外的寄存器。如果locspec解析为不同于当前执行的函数的地址，则如果两个函数期望不同的参数模式或本地变量，则结果可能是奇怪的。因此，如果跳转地址不在当前执行的函数中，跳转命令会要求确认。但是，即使是奇怪的结果，只要熟悉程序的机器语言代码，也是可以预测的。


On many systems, you can get much the same effect as the `jump` command by storing a new value into the register `$pc`. The difference is that this does not start your program running; it only changes the address of where it *will* run when you continue. For example,

> 在许多系统上，您可以通过将新值存储到寄存器$pc中来获得与`jump`命令类似的效果。不同之处在于，它不会启动您的程序运行；它只会在您继续时更改将要运行的地址。例如，

::: smallexample

```bash
set $pc = 0x485
```

:::


makes the next `continue` command or stepping command execute at address `0x485`, rather than at the address where your program stopped. See [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping).

> 让下一个`continue`命令或步进命令在地址`0x485`处执行，而不是在程序停止的地址处执行。详见[继续和步进](Continuing-and-Stepping.html#Continuing-and-Stepping)。


However, writing directly to `$pc` will only change the value of the program-counter register, while using `jump` will ensure that any additional auxiliary state is also updated. For example, on SPARC, `jump` will update both `$pc` and `$npc` registers prior to resuming execution. When using the approach of writing directly to `$pc` it is your job to also update the `$npc` register.

> 然而，直接写入`$pc`只会改变程序计数器寄存器的值，而使用`jump`将确保任何其他辅助状态也得到更新。例如，在SPARC上，`jump`将在恢复执行之前更新`$pc`和`$npc`寄存器。当使用直接写入`$pc`的方法时，您的任务是还要更新`$npc`寄存器。


The most common occasion to use the `jump` command is to back up---perhaps with more breakpoints set---over a portion of a program that has already executed, in order to examine its execution in more detail.

> 最常用的`跳转`命令是回溯——可能会设置更多断点——回溯已经执行过的程序的一部分，以便更详细地检查其执行情况。

---

::: header
Next: [Signaling](Signaling.html#Signaling)]
:::
