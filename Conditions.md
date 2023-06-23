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

This is the converse of using assertions for program validation; in that situation, you want to stop when the assertion is violated---that is, when the condition is false. In C, if you want to test an assertion expressed by the condition `assert`' on the appropriate breakpoint.

Conditions are also accepted for watchpoints; you may not need them, since a watchpoint is inspecting the value of an expression anyhow---but it might be simpler, say, to just set a watchpoint on a variable name, and specify a condition that tests whether the new value is an interesting one.

Break conditions can have side effects, and may even call functions in your program. This can be useful, for example, to activate functions that log program progress, or to use your own print functions to format special data structures. The effects are completely predictable unless there is another enabled breakpoint at the same address. (In that case, [GDB] might see the other breakpoint first and stop your program without checking the condition of this one.) Note that breakpoint commands are usually more convenient and flexible than break conditions for the purpose of performing side effects when a breakpoint is reached (see [Breakpoint Command Lists](Break-Commands.html#Break-Commands)).

Breakpoint conditions can also be evaluated on the target's side if the target supports it. Instead of evaluating the conditions locally, [GDB]. Global variables become raw memory locations, locals become stack accesses, and so forth.

In this case, [GDB] informed about every breakpoint trigger, even those with false conditions.

Break conditions can be specified when a breakpoint is set, by using '`if`' in the arguments to the `break` command. See [Setting Breakpoints](Set-Breaks.html#Set-Breaks). They can also be changed at any time with the `condition` command.

You can also use the `if` keyword with the `watch` command. The `catch` command does not recognize the `if` keyword; `condition` is the only way to impose a further condition on a catchpoint.

`condition bnum expression`

Specify `expression` prints an error message:

::: smallexample

```bash
No symbol "foo" in current context.
```

:::

[GDB] at the time the `condition` command (or a command that sets a breakpoint with a condition, like `break if …`) is given, however. See [Expressions](Expressions.html#Expressions).

`condition -force bnum expression`

When the `-force` flag is used, define the condition even if `expression`. This is similar to the `-force-condition` option of the `break` command.

`condition bnum`

Remove the condition from breakpoint number `bnum`. It becomes an ordinary unconditional breakpoint.

A special case of a breakpoint condition is to stop only when the breakpoint has been reached a certain number of times. This is so useful that there is a special way to do it, using the *ignore count* of the breakpoint. Every breakpoint has an ignore count, which is an integer. Most of the time, the ignore count is zero, and therefore has no effect. But if your program reaches a breakpoint whose ignore count is positive, then instead of stopping, it just decrements the ignore count by one and continues. As a result, if the ignore count value is `n` times your program reaches it.

`ignore bnum count`

Set the ignore count of breakpoint number `bnum` takes no action.

To make the breakpoint stop the next time it is reached, specify a count of zero.

When you use `continue` to resume execution of your program from a breakpoint, you can specify an ignore count directly as an argument to `continue`, rather than using `ignore`. See [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping).

If a breakpoint has a positive ignore count and a condition, the condition is not checked. Once the ignore count reaches zero, [GDB] resumes checking the condition.

You could achieve the effect of the ignore count with a condition such as '`$foo-- <= 0`' using a debugger convenience variable that is decremented each time. See [Convenience Variables](Convenience-Vars.html#Convenience-Vars).

Ignore counts apply to breakpoints, watchpoints, and catchpoints.

---

::: header
Next: [Break Commands](Break-Commands.html#Break-Commands)]
:::
