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

`jump locspec`

`j locspec`

Resume execution at the address of the code location that results from resolving `locspec` resolves to more than one address, those outside the current compilation unit are ignored. If considering just the addresses in the current compilation unit still doesn't yield a unique address, the command aborts before jumping. Execution stops again immediately if there is a breakpoint there. It is common practice to use the `tbreak` command in conjunction with `jump`. See [Setting Breakpoints](Set-Breaks.html#Set-Breaks).

The `jump` command does not change the current stack frame, or the stack pointer, or the contents of any memory location or any register other than the program counter. If `locspec` resolves to an address in a different function from the one currently executing, the results may be bizarre if the two functions expect different patterns of arguments or of local variables. For this reason, the `jump` command requests confirmation if the jump address is not in the function currently executing. However, even bizarre results are predictable if you are well acquainted with the machine-language code of your program.

On many systems, you can get much the same effect as the `jump` command by storing a new value into the register `$pc`. The difference is that this does not start your program running; it only changes the address of where it *will* run when you continue. For example,

::: smallexample

```bash
set $pc = 0x485
```

:::

makes the next `continue` command or stepping command execute at address `0x485`, rather than at the address where your program stopped. See [Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping).

However, writing directly to `$pc` will only change the value of the program-counter register, while using `jump` will ensure that any additional auxiliary state is also updated. For example, on SPARC, `jump` will update both `$pc` and `$npc` registers prior to resuming execution. When using the approach of writing directly to `$pc` it is your job to also update the `$npc` register.

The most common occasion to use the `jump` command is to back up---perhaps with more breakpoints set---over a portion of a program that has already executed, in order to examine its execution in more detail.

---

::: header
Next: [Signaling](Signaling.html#Signaling)]
:::
