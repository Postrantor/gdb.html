---
tip: translate by openai@2023-06-23 19:26:27
...
---
description: Conditions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Conditions (Debugging with GDB)
lang: en
resource-type: document
title: Conditions (Debugging with GDB)
---
::: header
Next: [Break Commands](Break-Commands.html#Break-Commands)]
:::

---

#### 5.1.6 Break Conditions


The simplest sort of breakpoint breaks every time your program reaches a specified place. You can also specify a *condition* for a breakpoint. A condition is just a Boolean expression in your programming language (see [Expressions](Expressions.html#Expressions)). A breakpoint with a condition evaluates the expression each time your program reaches it, and your program stops only if the condition is *true*.

> 最简单的断点每次程序到达指定位置时都会中断。您还可以为断点指定*条件*。条件只是您的编程语言中的布尔表达式（参见[表达式](Expressions.html#Expressions)）。带有条件的断点每次程序到达时都会评估表达式，只有当条件为*真*时，程序才会停止。


This is the converse of using assertions for program validation; in that situation, you want to stop when the assertion is violated---that is, when the condition is false. In C, if you want to test an assertion expressed by the condition `assert`' on the appropriate breakpoint.

> 这是使用断言进行程序验证的反向操作；在这种情况下，当断言被违反时，即条件为假时，你想要停止。在C中，如果你想要测试一个由条件`assert`表达的断言，请在适当的断点上进行。


Conditions are also accepted for watchpoints; you may not need them, since a watchpoint is inspecting the value of an expression anyhow---but it might be simpler, say, to just set a watchpoint on a variable name, and specify a condition that tests whether the new value is an interesting one.

> 条件也可以用于监视点；您可能不需要它们，因为监视点本身就在检查表达式的值---但可能会更简单，比如只设置一个变量名的监视点，并指定一个测试新值是否有趣的条件。


Break conditions can have side effects, and may even call functions in your program. This can be useful, for example, to activate functions that log program progress, or to use your own print functions to format special data structures. The effects are completely predictable unless there is another enabled breakpoint at the same address. (In that case, [GDB] might see the other breakpoint first and stop your program without checking the condition of this one.) Note that breakpoint commands are usually more convenient and flexible than break conditions for the purpose of performing side effects when a breakpoint is reached (see [Breakpoint Command Lists](Break-Commands.html#Break-Commands)).

> 断点条件可能会产生副作用，甚至可能调用程序中的函数。这可能很有用，例如，用于激活记录程序进度的功能，或者使用自己的打印函数来格式化特殊的数据结构。除非在相同地址处有另一个已启用的断点，否则效果是完全可预测的。（在这种情况下，[GDB]可能会首先看到另一个断点，而不会检查此断点的条件，从而停止程序。）请注意，对于在到达断点时执行副作用的目的，断点命令通常比断点条件更方便和灵活（请参阅[断点命令列表](Break-Commands.html#Break-Commands)）。


Breakpoint conditions can also be evaluated on the target's side if the target supports it. Instead of evaluating the conditions locally, [GDB]. Global variables become raw memory locations, locals become stack accesses, and so forth.

> 断点条件也可以在目标端评估，如果目标支持的话。而不是在本地评估条件，[GDB]。全局变量变成原始内存位置，本地变量变成堆栈访问等等。


In this case, [GDB] informed about every breakpoint trigger, even those with false conditions.

> 在这种情况下，GDB会通知每个断点触发，即使是那些具有错误条件的断点。


Break conditions can be specified when a breakpoint is set, by using '`if`' in the arguments to the `break` command. See [Setting Breakpoints](Set-Breaks.html#Set-Breaks). They can also be changed at any time with the `condition` command.

> 当设置断点时，可以使用“if”在`break`命令的参数中指定断点条件。请参阅[设置断点](Set-Breaks.html#Set-Breaks)。它们也可以随时使用`condition`命令更改。


You can also use the `if` keyword with the `watch` command. The `catch` command does not recognize the `if` keyword; `condition` is the only way to impose a further condition on a catchpoint.

> 你也可以使用`if`关键字和`watch`命令一起使用。`catch`命令不识别`if`关键字；`condition`是在catchpoint上施加进一步条件的唯一方式。

`condition bnum expression`

Specify `expression` prints an error message:

::: smallexample

```bash
No symbol "foo" in current context.
```

:::


[GDB] at the time the `condition` command (or a command that sets a breakpoint with a condition, like `break if …`) is given, however. See [Expressions](Expressions.html#Expressions).

> 当给出`condition`命令（或使用`break if...`之类的命令设置断点时，GDB会在此时进行评估。参见[表达式](Expressions.html#Expressions)。

`condition -force bnum expression`


When the `-force` flag is used, define the condition even if `expression`. This is similar to the `-force-condition` option of the `break` command.

> 当使用`-force`标志时，即使`expression`也定义条件。这类似于`break`命令的`-force-condition`选项。

`condition bnum`


Remove the condition from breakpoint number `bnum`. It becomes an ordinary unconditional breakpoint.

> 从断点编号`bnum`中移除条件，它变成一个普通的无条件断点。


A special case of a breakpoint condition is to stop only when the breakpoint has been reached a certain number of times. This is so useful that there is a special way to do it, using the *ignore count* of the breakpoint. Every breakpoint has an ignore count, which is an integer. Most of the time, the ignore count is zero, and therefore has no effect. But if your program reaches a breakpoint whose ignore count is positive, then instead of stopping, it just decrements the ignore count by one and continues. As a result, if the ignore count value is `n` times your program reaches it.

> 一种特殊的断点条件是只有当断点被达到某个特定的次数时才停止。这非常有用，因此有一种特殊的方法来做到这一点，使用断点的*忽略计数*。每个断点都有一个忽略计数，它是一个整数。大多数时候，忽略计数为零，因此没有任何效果。但是，如果您的程序到达其忽略计数为正的断点，那么它不会停止，而是将忽略计数减少1，然后继续执行。因此，如果忽略计数值为`n`次，则您的程序将到达该断点。

`ignore bnum count`

Set the ignore count of breakpoint number `bnum` takes no action.


To make the breakpoint stop the next time it is reached, specify a count of zero.

> 要让断点在下次被触发时停止，请指定一个零计数。


When you use `continue` to resume execution of your program from a breakpoint, you can specify an ignore count directly as an argument to `continue`, rather than using `ignore`. See [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping).

> 当你使用`continue`从断点处恢复程序执行时，你可以直接将忽略计数作为`continue`的参数，而不是使用`ignore`。详见 [继续和步进](Continuing-and-Stepping.html#Continuing-and-Stepping)。


If a breakpoint has a positive ignore count and a condition, the condition is not checked. Once the ignore count reaches zero, [GDB] resumes checking the condition.

> 如果断点具有正的忽略计数和条件，则不检查该条件。一旦忽略计数达到零，[GDB]将恢复检查条件。


You could achieve the effect of the ignore count with a condition such as '`$foo-- <= 0`' using a debugger convenience variable that is decremented each time. See [Convenience Variables](Convenience-Vars.html#Convenience-Vars).

> 你可以使用调试器便利变量，每次减少一次，使用'$foo-- <= 0'这样的条件来实现忽略计数的效果。参见[便利变量](Convenience-Vars.html#Convenience-Vars)。

Ignore counts apply to breakpoints, watchpoints, and catchpoints.

---

::: header
Next: [Break Commands](Break-Commands.html#Break-Commands)]
:::
