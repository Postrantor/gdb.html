---
tip: translate by openai@2023-06-23 18:26:14
...
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

> 一些处理器架构对可以放置断点的地址施加限制。对于这样受限的架构，[GDB]将尝试调整断点的地址以符合架构规定的限制。


One example of such an architecture is the Fujitsu FR-V. The FR-V is a VLIW architecture in which a number of RISC-like instructions may be bundled together for parallel execution. The FR-V architecture constrains the location of a breakpoint instruction within such a bundle to the instruction with the lowest address. [GDB] honors this constraint by adjusting a breakpoint's address to the first in the bundle.

> 一个这样的架构的例子是富士通FR-V。FR-V是一种VLIW架构，可以将许多类似RISC的指令捆绑在一起进行并行执行。FR-V架构将断点指令的位置限制在具有最低地址的指令中。[GDB]通过调整断点的地址来遵守这一约束。


It is not uncommon for optimized code to have bundles which contain instructions from different source statements, thus it may happen that a breakpoint's address will be adjusted from one source statement to another. Since this adjustment may significantly alter [GDB]'s breakpoint related behavior from what the user expects, a warning is printed when the breakpoint is first set and also when the breakpoint is hit.

> 不少得到优化的代码都会有包含来自不同源语句的指令的捆绑，因此断点的地址可能会从一个源语句调整到另一个源语句。由于这种调整可能会显著改变用户期望的[GDB]的断点相关行为，因此在首次设置断点时以及在断点被击中时都会打印出警告。


A warning like the one below is printed when setting a breakpoint that's been subject to address adjustment:

> 当设置受地址调整影响的断点时，将打印类似以下警告：

::: smallexample

```bash
warning: Breakpoint address adjusted from 0x00010414 to 0x00010410.
```

:::


Such warnings are printed both for user settable and [GDB]'s internal breakpoints. If you see one of these warnings, you should verify that a breakpoint set at the adjusted address will have the desired affect. If not, the breakpoint in question may be removed and other breakpoints may be set which will have the desired behavior. E.g., it may be sufficient to place the breakpoint at a later instruction. A conditional breakpoint may also be useful in some cases to prevent the breakpoint from triggering too often.

> 这些警告既适用于用户可设置的断点，也适用于GDB的内部断点。如果您看到其中之一的警告，应该验证在调整后的地址设置断点是否能达到预期的效果。如果不能，可以移除该断点，并设置其他断点以达到预期的行为。例如，可能只需要将断点设置在更晚的指令处就可以了。在某些情况下，也可以使用条件断点来防止断点过于频繁地触发。


[GDB] will also issue a warning when stopping at one of these adjusted breakpoints:

> [GDB] 在停止在这些调整后的断点处时也会发出警告。

::: smallexample

```bash
warning: Breakpoint 1 address previously adjusted from 0x00010414
to 0x00010410.
```

:::


When this warning is encountered, it may be too late to take remedial action except in cases where the breakpoint is hit earlier or more frequently than expected.

> 当遇到这个警告时，除非断点比预期更早或更频繁地被命中，否则采取补救措施可能已经太晚了。

---

::: header
Previous: [Error in Breakpoints](Error-in-Breakpoints.html#Error-in-Breakpoints)]
:::
