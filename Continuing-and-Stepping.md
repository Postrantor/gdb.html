---
tip: translate by openai@2023-06-23 19:37:50
...
---
description: Continuing and Stepping (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Continuing and Stepping (Debugging with GDB)
lang: en
resource-type: document
title: Continuing and Stepping (Debugging with GDB)
---
::: header
Next: [Skipping Over Functions and Files](Skipping-Over-Functions-and-Files.html#Skipping-Over-Functions-and-Files)]
:::

---

### 5.2 Continuing and Stepping


*Continuing* means resuming program execution until your program completes normally. In contrast, *stepping* means executing just one more "step" of your program, where "step" may mean either one line of source code, or one machine instruction (depending on what particular command you use). Either when continuing or when stepping, your program may stop even sooner, due to a breakpoint or a signal. (If it stops due to a signal, you may want to use `handle`, or use '`signal 0`' to resume execution (see [Signals](Signals.html#Signals)), or you may step into the signal's handler (see [stepping and signal handlers](Signals.html#stepping-and-signal-handlers)).)

> 继续意味着继续执行程序，直到程序正常完成。相反，步进意味着只执行程序的一个“步骤”，其中“步骤”可以是一行源代码或一个机器指令（取决于您使用的特定命令）。无论是继续还是步进，程序由于断点或信号而可能更早地停止。（如果它由于信号而停止，您可能想使用“handle”或使用“signal 0”来恢复执行（参见[信号]（Signals.html#Signals）），或者您可以步入信号处理程序（参见[步进和信号处理程序]（Signals.html#stepping-and-signal-handlers）））。

`continue [ignore-count]`

`c [ignore-count]`

`fg [ignore-count]`


Resume program execution, at the address where your program last stopped; any breakpoints set at that address are bypassed. The optional argument `ignore-count` allows you to specify a further number of times to ignore a breakpoint at this location; its effect is like that of `ignore` (see [Break Conditions](Conditions.html#Conditions)).

> 恢复程序执行，从程序上次停止的地址开始；在该地址设置的任何断点都将被忽略。可选参数`ignore-count`允许您指定进一步忽略此位置上断点的次数；它的效果类似于[断点条件]（Conditions.html#Conditions）中的`ignore`。


The argument `ignore-count` is meaningful only when your program stopped due to a breakpoint. At other times, the argument to `continue` is ignored.

> 参数`ignore-count`只有在程序因断点而停止时才有意义。在其他时候，`continue`的参数将被忽略。


The synonyms `c` and `fg` (for *foreground*, as the debugged program is deemed to be the foreground program) are provided purely for convenience, and have exactly the same behavior as `continue`.

> `c`和`fg`（用作*前景*，因为调试的程序被视为前景程序）的同义词仅提供方便，与`继续`的行为完全相同。


To resume execution at a different place, you can use `return` (see [Returning from a Function](Returning.html#Returning)) to go back to the calling function; or `jump` (see [Continuing at a Different Address](Jumping.html#Jumping)) to go to an arbitrary location in your program.

> 重新开始执行程序的不同位置，可以使用`return`（参见[从函数返回](Returning.html#Returning)）返回调用函数；或者使用`jump`（参见[在不同地址继续](Jumping.html#Jumping)）跳转到程序的任意位置。


A typical technique for using stepping is to set a breakpoint (see [Breakpoints; Watchpoints; and Catchpoints](Breakpoints.html#Breakpoints)) at the beginning of the function or the section of your program where a problem is believed to lie, run your program until it stops at that breakpoint, and then step through the suspect area, examining the variables that are interesting, until you see the problem happen.

> 一种典型的使用步进的技术是在函数开头或程序中可能存在问题的部分设置断点（参见[断点; 监视点; 和捕获点](Breakpoints.html#Breakpoints))，运行程序直到它在该断点处停止，然后步进可疑区域，检查有趣的变量，直到看到问题发生。

`step`


Continue running your program until control reaches a different source line, then stop it and return control to [GDB]. This command is abbreviated `s`.

> 继续运行程序，直到控制权到达不同的源行，然后停止它并将控制权返回给[GDB]。此命令缩写为`s`。

> *Warning:* If you use the `step` command while control is within a function that was compiled without debugging information, execution proceeds until control reaches a function that does have debugging information. Likewise, it will not step into a function which is compiled without debugging information. To step through functions without debugging information, use the `stepi` command, described below.


The `step` command only stops at the first instruction of a source line. This prevents the multiple stops that could otherwise occur in `switch` statements, `for` loops, etc. `step` continues to stop if a function that has debugging information is called within the line. In other words, `step` *steps inside* any functions called within the line.

> `step` 命令仅在源代码行的第一个指令处停止。这可以防止`switch`语句、`for`循环等可能发生的多次停止。如果在行内调用具有调试信息的函数，`step`将继续停止。换句话说，`step`会在行内调用的任何函数*内部步进*。


Also, the `step` command only enters a function if there is line number information for the function. Otherwise it acts like the `next` command. This avoids problems when using `cc -gl` on MIPS machines. Previously, `step` entered subroutines if there was any debugging information about the routine.

> 此外，`step` 命令只有在函数有行号信息时才会进入该函数，否则它的行为就像`next` 命令一样。这样可以避免在 MIPS 机器上使用 `cc -gl` 时出现问题。以前，`step` 如果有任何关于该例程的调试信息，就会进入子程序。

`step count`


Continue running as in `step`, but do so `count` steps, stepping stops right away.

> 继续按照`步骤`的方式运行，但运行`计数`步，跳步立即停止。

`next [count]`


Continue to the next source line in the current (innermost) stack frame. This is similar to `step`, but function calls that appear within the line of code are executed without stopping. Execution stops when control reaches a different line of code at the original stack level that was executing when you gave the `next` command. This command is abbreviated `n`.

> 继续到当前（最内层）堆栈帧中的下一个源代码行。这与`step`类似，但代码行中出现的函数调用将在不停止的情况下执行。当控制到达您给出`next`命令时正在执行的原始堆栈级别的不同代码行时，执行将停止。此命令缩写为`n`。

An argument `count` is a repeat count, as for `step`.


The `next` command only stops at the first instruction of a source line. This prevents multiple stops that could otherwise occur in `switch` statements, `for` loops, etc.

> 下一条命令只会在源代码行的第一条指令处停止。这可以防止`switch`语句、`for`循环等可能发生的多次停止。

`set step-mode`

`set step-mode on`


The `set step-mode on` command causes the `step` command to stop at the first instruction of a function which contains no debug line information rather than stepping over it.

> 命令`set step-mode on`会导致`step`命令在没有调试行信息的函数的第一条指令处停止，而不是跳过它。


This is useful in cases where you may be interested in inspecting the machine instructions of a function which has no symbolic info and do not want [GDB] to automatically skip over this function.

> 这在您可能有兴趣检查没有符号信息的函数的机器指令，而不希望[GDB]自动跳过此函数的情况下很有用。

`set step-mode off`


Causes the `step` command to step over any functions which contains no debug information. This is the default.

> `step` 命令会跳过没有调试信息的函数，这是默认行为。

`show step-mode`


Show whether [GDB] will stop in or step over functions without source line debug information.

> 检查GDB是否会在没有源代码调试信息的情况下停止或跳过函数。

`finish`


Continue running until just after function in the selected stack frame returns. Print the returned value (if any). This command can be abbreviated as `fin`.

> 继续运行，直到在所选堆栈帧中函数返回之后。打印返回值（如果有）。此命令可缩写为`fin`。


Contrast this with the `return` command (see [Returning from a Function](Returning.html#Returning)).

> 与`return`命令进行对比（参见[从函数返回]（Returning.html#Returning））。

`set print finish [on|off]`

`show print finish`


By default the `finish` command will show the value that is returned by the function. This can be disabled using `set print finish off`. When disabled, the value is still entered into the value history (see [Value History](Value-History.html#Value-History)), but not displayed.

> 默认情况下，`finish`命令会显示函数返回的值。可以使用`set print finish off`禁用这个功能。禁用后，该值仍会被记录到值历史（参见[值历史](Value-History.html#Value-History）），但不会显示出来。

`until`

`u`


Continue running until a source line past the current line, in the current stack frame, is reached. This command is used to avoid single stepping through a loop more than once. It is like the `next` command, except that when `until` encounters a jump, it automatically continues execution until the program counter is greater than the address of the jump.

> 继续运行，直到到达当前堆栈帧中的当前行之后的源行。此命令用于避免多次单步调试循环。它与`next`命令类似，但是当`until`遇到跳转时，它会自动继续执行，直到程序计数器大于跳转的地址。


This means that when you reach the end of a loop after single stepping though it, `until` makes your program continue execution until it exits the loop. In contrast, a `next` command at the end of a loop simply steps back to the beginning of the loop, which forces you to step through the next iteration.

> 这意味着，当您在单步执行循环后到达循环结尾时，`until` 会使您的程序继续执行，直到它退出循环。相比之下，循环末尾的`next`命令只会将您退回到循环开头，这迫使您跨越下一次迭代。

`until` always stops your program if it attempts to exit the current stack frame.

`until` may produce somewhat counterintuitive results if the order of machine code does not match the order of the source lines. For example, in the following excerpt from a debugging session, the `f` (`frame`) command shows that execution is stopped at line `206`; yet when we use `until`, we get to line `195`:

::: smallexample

```bash
(gdb) f
#0  main (argc=4, argv=0xf7fffae8) at m4.c:206
206                 expand_input();
(gdb) until
195             for ( ; argc > 0; NEXTARG) {
```

:::


This happened because, for execution efficiency, the compiler had generated code for the loop closure test at the end, rather than the start, of the loop---even though the test in a C `for`-loop is written before the body of the loop. The `until` command appeared to step back to the beginning of the loop when it advanced to this expression; however, it has not really gone to an earlier statement---not in terms of the actual machine code.

> 这是因为，为了执行效率，编译器在循环的末尾而不是开头生成了循环结束测试的代码 - 尽管C中的`for`循环的测试是在循环体之前编写的。`until`命令似乎在它跳转到这个表达式时回到了循环的开头；但是它实际上并没有回到早期的语句 - 就机器码而言。

`until` with no argument works by means of single instruction stepping, and hence is slower than `until` with an argument.

`until locspec`

`u locspec`


Continue running your program until either it reaches a code location that results from resolving `locspec` is any of the forms described in [Location Specifications](Location-Specifications.html#Location-Specifications). This form of the command uses temporary breakpoints, and hence is quicker than `until` without an argument. The specified location is actually reached only if it is in the current frame. This implies that `until` can be used to skip over recursive function invocations. For instance in the code below, if the current location is line `96`, issuing `until 99` will execute the program up to line `99` in the same invocation of factorial, i.e., after the inner invocations have returned.

> 继续运行你的程序，直到它到达从解析`locspec`得到的代码位置，这是[位置规范](Location-Specifications.html#Location-Specifications)中描述的任何形式。这种命令使用临时断点，因此比没有参数的`until`更快。只有在当前帧中到达指定位置时，指定位置才实际到达。这意味着`until`可以用来跳过递归函数调用。例如，在下面的代码中，如果当前位置是第96行，输入`until 99`将执行程序到同一次调用的阶乘的第99行，即内部调用返回后。

::: smallexample

```bash
94    int factorial (int value)
95  {
96      if (value > 1) {
97            value *= factorial (value - 1);
98      }
99      return (value);
100     }
```

:::

`advance locspec`


Continue running your program until either it reaches a code location that results from resolving `locspec` is any of the forms described in [Location Specifications](Location-Specifications.html#Location-Specifications). This command is similar to `until`, but `advance` will not skip over recursive function calls, and the target code location doesn't have to be in the same frame as the current one.

> 继续运行您的程序，直到它到达从解析`locspec`得出的代码位置，这个形式在[位置规范]（Location-Specifications.html＃Location-Specifications）中有描述。此命令类似于`until`，但`advance`不会跳过递归函数调用，而目标代码位置不必与当前位置在同一帧中。

`stepi`

`stepi arg`

`si`

Execute one machine instruction, then stop and return to the debugger.


It is often useful to do '`display/i $pc` automatically display the next instruction to be executed, each time your program stops. See [Automatic Display](Auto-Display.html#Auto-Display).

> 常常有用的是每次程序停止时自动执行'display/i $pc'以显示下一条要执行的指令。请参阅[自动显示](Auto-Display.html#Auto-Display)。

An argument is a repeat count, as in `step`.

`nexti`

`nexti arg`

`ni`


Execute one machine instruction, but if it is a function call, proceed until the function returns.

> 执行一条机器指令，如果它是一个函数调用，继续执行直到函数返回。

An argument is a repeat count, as in `next`.


By default, and if available, [GDB] could make line stepping behave incorrectly when target-assisted range stepping is enabled. You can use the following command to turn off range stepping if necessary:

> 默认情况下，如果可用，GDB可能会在启用目标协助范围步进时导致行步进行为不正确。如果需要，可以使用以下命令关闭范围步进：

`set range-stepping`

`show range-stepping`

Control whether range stepping is enabled.


If `on`, and the target supports it, [GDB] always issues single-steps, even if range stepping is supported by the target. The default is `on`.

> 如果设置为“on”，并且目标支持它，[GDB]总是发出单步指令，即使目标支持范围步进也是如此。默认设置为“on”。

---

::: header
Next: [Skipping Over Functions and Files](Skipping-Over-Functions-and-Files.html#Skipping-Over-Functions-and-Files)]
:::
