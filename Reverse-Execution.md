---
tip: translate by openai@2023-06-23 12:28:37
...
---
description: Reverse Execution (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Reverse Execution (Debugging with GDB)
lang: en
resource-type: document
title: Reverse Execution (Debugging with GDB)
---------------------------------------------

::: header
Next: [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)]
:::

---

## 6 Running programs backward

When you are debugging a program, it is not unusual to realize that you have gone too far, and some event of interest has already happened. If the target environment supports it, [GDB] can allow you to "rewind" the program by running it backward.

> 当你在调试一个程序时，你会发现你已经走得太远，并且一些感兴趣的事件已经发生了。如果目标环境支持，[GDB]可以允许你通过倒带的方式来重新运行程序。

A target environment that supports reverse execution should be able to "undo" the changes in machine state that have taken place as the program was executing normally. Variables, registers etc. should revert to their previous values. Obviously this requires a great deal of sophistication on the part of the target environment; not all target environments can support reverse execution.

> 一个支持反向执行的目标环境应该能够"撤消"程序正常执行时发生的机器状态的更改。变量、寄存器等应该恢复到他们之前的值。显然，这需要目标环境具有很强的复杂性；并不是所有的目标环境都能支持反向执行。

When a program is executed in reverse, the instructions that have most recently been executed are "un-executed", in reverse order. The program counter runs backward, following the previous thread of execution in reverse. As each instruction is "un-executed", the values of memory and/or registers that were changed by that instruction are reverted to their previous states. After executing a piece of source code in reverse, all side effects of that code should be "undone", and all variables should be returned to their prior values[^7^](#FOOT7).

> 当程序反向执行时，最近执行的指令将被“反执行”，以相反的顺序执行。程序计数器向后走，按照之前的执行线程反向执行。当每条指令被“反执行”时，由该指令改变的内存和/或寄存器的值将被恢复到先前的状态。在反向执行源代码之后，所有副作用应该被“撤销”，所有变量应该恢复到先前的值。

On some platforms, [GDB] has built-in support for reverse execution, activated with the `record` or `record btrace` commands. See [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay). Some remote targets, typically full system emulators, support reverse execution directly without requiring any special command.

> 在某些平台上，[GDB]有内置的反向执行支持，可以通过 `record` 或 `record btrace` 命令激活。参见[进程记录和重放](Process-Record-and-Replay.html#Process-Record-and-Replay)。一些远程目标，通常是全系统模拟器，可以直接支持反向执行，而不需要任何特殊命令。

If you are debugging in a target environment that supports reverse execution, [GDB] provides the following commands.

> 如果您在支持反向执行的目标环境中进行调试，[GDB]提供以下命令。

`reverse-continue [ignore-count]`

`rc [ignore-count]`

Beginning at the point where your program last stopped, start executing in reverse. Reverse execution will stop for breakpoints and synchronous exceptions (signals), just like normal execution. Behavior of asynchronous signals depends on the target environment.

> 从程序上次停止的位置开始，以相反的顺序执行。断点和同步异常（信号）会停止反向执行，就像正常执行一样。异步信号的行为取决于目标环境。

`reverse-step [count]`

Run the program backward until control reaches the start of a different source line; then stop it, and return control to [GDB].

> 运行程序直到控制到达另一个源代码行的开头；然后停止它，并将控制返回给[GDB]。

Like the `step` command, `reverse-step` will only stop at the beginning of a source line. It "un-executes" the previously executed source line. If the previous source line included calls to debuggable functions, `reverse-step` will step (backward) into the called function, stopping at the beginning of the *last* statement in the called function (typically a return statement).

> 就像 `step` 命令一样，`reverse-step` 只会停留在源代码行的开头。它会"反执行"之前执行的源代码行。如果之前的源代码行包含调用可调试的函数，`reverse-step` 会（向后）步入调用的函数，停留在调用函数中*最后*一条语句（通常是一个返回语句）的开头。

Also, as with the `step` command, if non-debuggable functions are called, `reverse-step` will run thru them backward without stopping.

> 此外，就像 `step` 命令一样，如果调用了不可调试的函数，`reverse-step` 将以倒序方式运行而不会停止。

`reverse-stepi [count]`

Reverse-execute one machine instruction. Note that the instruction to be reverse-executed is *not* the one pointed to by the program counter, but the instruction executed prior to that one. For instance, if the last instruction was a jump, `reverse-stepi` will take you back from the destination of the jump to the jump instruction itself.

> 反向执行一条机器指令。注意，要反向执行的指令*不*是程序计数器指向的指令，而是在该指令之前执行的指令。例如，如果最后一条指令是跳转，`reverse-stepi` 将使您从跳转目标返回跳转指令本身。

`reverse-next [count]`

Run backward to the beginning of the previous line executed in the current (innermost) stack frame. If the line contains function calls, they will be "un-executed" without stopping. Starting from the first line of a function, `reverse-next` will take you back to the caller of that function, *before* the function was called, just as the normal `next` command would take you from the last line of a function back to its return to its caller [^8^](#FOOT8).

> 在当前（最内层）堆栈帧中运行回到上一行开头。如果行包含函数调用，它们将在不停止的情况下被“反执行”。从函数的第一行开始，`reverse-next` 将带您回到调用该函数的调用者，就像正常的 `next` 命令将从函数的最后一行回到其返回到其调用者一样[^8^]（#FOOT8）。

`reverse-nexti [count]`

Like `nexti`, `reverse-nexti` executes a single instruction in reverse, except that called functions are "un-executed" atomically. That is, if the previously executed instruction was a return from another function, `reverse-nexti` will continue to execute in reverse until the call to that function (from the current stack frame) is reached.

> 就像 `nexti` 一样，`reverse-nexti` 以反向执行单条指令，但被调用的函数会以“原子”方式“未执行”。也就是说，如果先前执行的指令是从另一个函数返回，`reverse-nexti` 将继续以反向方式执行，直到到达从当前堆栈帧调用该函数的位置。

`reverse-finish`

Just as the `finish` command takes you to the point where the current function returns, `reverse-finish` takes you to the point where it was called. Instead of ending up at the end of the current function invocation, you end up at the beginning.

> 就像 `finish` 命令带你到当前函数返回的点，`reverse-finish` 带你到它被调用的点。不是最终到达当前函数调用的结尾，而是到达开头。

`set exec-direction`

Set the direction of target execution.

> 设定目标执行的方向。

`set exec-direction reverse`

[GDB] will perform all execution commands in reverse, until the exec-direction mode is changed to "forward". Affected commands include `step, stepi, next, nexti, continue, and finish`. The `return` command cannot be used in reverse mode.

> [GDB] 将按照相反的顺序执行所有执行命令，直到执行方向模式更改为“正向”。受影响的命令包括“step”，“stepi”，“next”，“nexti”，“continue”和“finish”。在反向模式中不能使用“return”命令。

`set exec-direction forward`

[GDB] will perform all execution commands in the normal fashion. This is the default.

> GDB 将以正常的方式执行所有执行命令。这是默认设置。

::: footnote

---

#### Footnotes

### [(7)](#DOCF7)

Note that some side effects are easier to undo than others. For instance, memory and registers are relatively easy, but device I/O is hard. Some targets may be able undo things like device I/O, and some may not.

The contract between [GDB] accepts whatever it is given.

> 合同在[GDB]之间接受任何它被给予的东西。

### [(8)](#DOCF8)

Unless the code is too heavily optimized.

> 除非代码优化得太多。
> :::

---

::: header
Next: [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)]
:::
