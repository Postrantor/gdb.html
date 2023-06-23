---
description: Breakpoint-related Warnings (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Breakpoint-related Warnings (Debugging with GDB)
lang: en
resource-type: document
title: Breakpoint-related Warnings (Debugging with GDB)
---
::: header
Previous: [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints)]
:::

---

#### 5.1.12 "Breakpoint address adjusted\..."

Some processor architectures place constraints on the addresses at which breakpoints may be placed. For architectures thus constrained, [GDB] will attempt to adjust the breakpoint's address to comply with the constraints dictated by the architecture.

One example of such an architecture is the Fujitsu FR-V. The FR-V is a VLIW architecture in which a number of RISC-like instructions may be bundled together for parallel execution. The FR-V architecture constrains the location of a breakpoint instruction within such a bundle to the instruction with the lowest address. [GDB] honors this constraint by adjusting a breakpoint's address to the first in the bundle.

It is not uncommon for optimized code to have bundles which contain instructions from different source statements, thus it may happen that a breakpoint's address will be adjusted from one source statement to another. Since this adjustment may significantly alter [GDB]'s breakpoint related behavior from what the user expects, a warning is printed when the breakpoint is first set and also when the breakpoint is hit.

A warning like the one below is printed when setting a breakpoint that's been subject to address adjustment:

::: smallexample

```bash
warning: Breakpoint address adjusted from 0x00010414 to 0x00010410.
```

:::

Such warnings are printed both for user settable and [GDB]'s internal breakpoints. If you see one of these warnings, you should verify that a breakpoint set at the adjusted address will have the desired affect. If not, the breakpoint in question may be removed and other breakpoints may be set which will have the desired behavior. E.g., it may be sufficient to place the breakpoint at a later instruction. A conditional breakpoint may also be useful in some cases to prevent the breakpoint from triggering too often.

[GDB] will also issue a warning when stopping at one of these adjusted breakpoints:

::: smallexample

```bash
warning: Breakpoint 1 address previously adjusted from 0x00010414
to 0x00010410.
```

:::

When this warning is encountered, it may be too late to take remedial action except in cases where the breakpoint is hit earlier or more frequently than expected.

---

::: header
Previous: [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints)]
:::
