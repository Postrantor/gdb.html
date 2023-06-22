---
description: Reverse Execution (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Reverse Execution (Debugging with GDB)
lang: en
resource-type: document
title: Reverse Execution (Debugging with GDB)
---
::: header
Next: [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)]
:::

---

## 6 Running programs backward

When you are debugging a program, it is not unusual to realize that you have gone too far, and some event of interest has already happened. If the target environment supports it, [GDB] can allow you to "rewind" the program by running it backward.

A target environment that supports reverse execution should be able to "undo" the changes in machine state that have taken place as the program was executing normally. Variables, registers etc. should revert to their previous values. Obviously this requires a great deal of sophistication on the part of the target environment; not all target environments can support reverse execution.

When a program is executed in reverse, the instructions that have most recently been executed are "un-executed", in reverse order. The program counter runs backward, following the previous thread of execution in reverse. As each instruction is "un-executed", the values of memory and/or registers that were changed by that instruction are reverted to their previous states. After executing a piece of source code in reverse, all side effects of that code should be "undone", and all variables should be returned to their prior values[^7^](#FOOT7).

On some platforms, [GDB] has built-in support for reverse execution, activated with the `record` or `record btrace` commands. See [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay). Some remote targets, typically full system emulators, support reverse execution directly without requiring any special command.

If you are debugging in a target environment that supports reverse execution, [GDB] provides the following commands.

`reverse-continue [ignore-count]`

`rc [ignore-count]`

Beginning at the point where your program last stopped, start executing in reverse. Reverse execution will stop for breakpoints and synchronous exceptions (signals), just like normal execution. Behavior of asynchronous signals depends on the target environment.

`reverse-step [count]`

Run the program backward until control reaches the start of a different source line; then stop it, and return control to [GDB].

Like the `step` command, `reverse-step` will only stop at the beginning of a source line. It "un-executes" the previously executed source line. If the previous source line included calls to debuggable functions, `reverse-step` will step (backward) into the called function, stopping at the beginning of the *last* statement in the called function (typically a return statement).

Also, as with the `step` command, if non-debuggable functions are called, `reverse-step` will run thru them backward without stopping.

`reverse-stepi [count]`

Reverse-execute one machine instruction. Note that the instruction to be reverse-executed is *not* the one pointed to by the program counter, but the instruction executed prior to that one. For instance, if the last instruction was a jump, `reverse-stepi` will take you back from the destination of the jump to the jump instruction itself.

`reverse-next [count]`

Run backward to the beginning of the previous line executed in the current (innermost) stack frame. If the line contains function calls, they will be "un-executed" without stopping. Starting from the first line of a function, `reverse-next` will take you back to the caller of that function, *before* the function was called, just as the normal `next` command would take you from the last line of a function back to its return to its caller [^8^](#FOOT8).

`reverse-nexti [count]`

Like `nexti`, `reverse-nexti` executes a single instruction in reverse, except that called functions are "un-executed" atomically. That is, if the previously executed instruction was a return from another function, `reverse-nexti` will continue to execute in reverse until the call to that function (from the current stack frame) is reached.

`reverse-finish`

Just as the `finish` command takes you to the point where the current function returns, `reverse-finish` takes you to the point where it was called. Instead of ending up at the end of the current function invocation, you end up at the beginning.

`set exec-direction`

Set the direction of target execution.

`set exec-direction reverse`

[GDB] will perform all execution commands in reverse, until the exec-direction mode is changed to "forward". Affected commands include `step, stepi, next, nexti, continue, and finish`. The `return` command cannot be used in reverse mode.

`set exec-direction forward`

[GDB] will perform all execution commands in the normal fashion. This is the default.

::: footnote

---

#### Footnotes

### [(7)](#DOCF7)

Note that some side effects are easier to undo than others. For instance, memory and registers are relatively easy, but device I/O is hard. Some targets may be able undo things like device I/O, and some may not.

The contract between [GDB] accepts whatever it is given.

### [(8)](#DOCF8)

Unless the code is too heavily optimized.
:::

---

::: header
Next: [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay)]
:::
