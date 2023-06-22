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

::: smallexample

```bash
(gdb) watch address|variable \
  if  address|variable == constant expression
```

:::

The DVC register will be automatically used when [GDB] running on a Linux kernel version 2.6.34 or newer.

When running on PowerPC embedded processors, [GDB] automatically uses ranged hardware watchpoints, unless the `exact-watchpoints` option is on, in which case watchpoints using only one debug register are created when watching variables of scalar types.

You can create an artificial array to watch an arbitrary memory region using one of the following commands (see [Expressions](Expressions.html#Expressions)):

::: smallexample

```bash
(gdb) watch *((char *) address)@length
(gdb) watch  address
```

:::

PowerPC embedded processors support masked watchpoints. See the discussion about the `mask` argument in [Set Watchpoints](Set-Watchpoints.html#Set-Watchpoints).

PowerPC embedded processors support hardware accelerated *ranged breakpoints*. A ranged breakpoint stops execution of the inferior whenever it executes an instruction at any address within the range it was set at. To set a ranged breakpoint in [GDB], use the `break-range` command.

[GDB] provides the following PowerPC-specific commands:

`break-range start-locspec, end-locspec`

Set a breakpoint for an address range given by `start-locspec` resolve to multiple code locations in the program, then the command aborts with an error without creating a breakpoint.

`set powerpc soft-float`

`show powerpc soft-float`

Force [GDB] selects the calling convention based on the selected architecture and the provided executable file.

`set powerpc vector-abi`

`show powerpc vector-abi`

Force [GDB] selects the calling convention based on the selected architecture and the provided executable file.

`set powerpc exact-watchpoints`

`show powerpc exact-watchpoints`

Allow [GDB] to use only one debug register when watching a variable of scalar type, thus assuming that the variable is accessed through the address of its first byte.

---

::: header
Next: [AVR](AVR.html#AVR)]
:::
