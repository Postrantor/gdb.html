---
tip: translate by openai@2023-06-23 17:06:13
...
---
description: Agent Expressions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Agent Expressions (Debugging with GDB)
lang: en
resource-type: document
title: Agent Expressions (Debugging with GDB)
---
::: header
Next: [Target Descriptions](Target-Descriptions.html#Target-Descriptions)]
:::

---

## Appendix F The GDB Agent Expression Mechanism


In some applications, it is not feasible for the debugger to interrupt the program's execution long enough for the developer to learn anything helpful about its behavior. If the program's correctness depends on its real-time behavior, delays introduced by a debugger might cause the program to fail, even when the code itself is correct. It is useful to be able to observe the program's behavior without interrupting it.

> 在一些应用中，调试器中断程序执行的时间不足以让开发者有所帮助，因此不可行。如果程序的正确性取决于它的实时行为，调试器引入的延迟可能会导致程序失败，即使代码本身是正确的。能够观察程序的行为而不中断它是很有用的。


Using GDB's `trace` and `collect` commands, the user can specify locations in the program, and arbitrary expressions to evaluate when those locations are reached. Later, using the `tfind` command, she can examine the values those expressions had when the program hit the trace points. The expressions may also denote objects in memory --- structures or arrays, for example --- whose values GDB should record; while visiting a particular tracepoint, the user may inspect those objects as if they were in memory at that moment. However, because GDB records these values without interacting with the user, it can do so quickly and unobtrusively, hopefully not disturbing the program's behavior.

> 使用GDB的`trace`和`collect`命令，用户可以指定程序中的位置和到达这些位置时要评估的任意表达式。之后，使用`tfind`命令，她可以检查程序到达跟踪点时这些表达式的值。这些表达式也可以表示内存中的对象，例如结构或数组，GDB应该记录它们的值；当访问特定的跟踪点时，用户可以像当时内存中一样检查这些对象。但是，由于GDB在不与用户交互的情况下记录这些值，因此可以快速而不显眼地进行，希望不会打扰程序的行为。


When GDB is debugging a remote target, the GDB *agent* code running on the target computes the values of the expressions itself. To avoid having a full symbolic expression evaluator on the agent, GDB translates expressions in the source language into a simpler bytecode language, and then sends the bytecode to the agent; the agent then executes the bytecode, and records the values for GDB to retrieve later.

> 当GDB在调试远程目标时，运行在目标上的GDB *代理*代码计算表达式的值本身。为了避免在代理上有一个完整的符号表达式求值器，GDB将源语言中的表达式转换为一种更简单的字节码语言，然后将字节码发送到代理；代理然后执行字节码，并记录GDB以便稍后检索的值。


The bytecode language is simple; there are forty-odd opcodes, the bulk of which are the usual vocabulary of C operands (addition, subtraction, shifts, and so on) and various sizes of literals and memory reference operations. The bytecode interpreter operates strictly on machine-level values --- various sizes of integers and floating point numbers --- and requires no information about types or symbols; thus, the interpreter's internal data structures are simple, and each bytecode requires only a few native machine instructions to implement it. The interpreter is small, and strict limits on the memory and time required to evaluate an expression are easy to determine, making it suitable for use by the debugging agent in real-time applications.

> 字节码语言简单；有四十多条操作码，其中大多数是C运算符的常用词汇（加法，减法，移位等）以及各种大小的文字和内存引用操作。字节码解释器严格地操作机器级值，即各种大小的整数和浮点数，无需关于类型或符号的信息；因此，解释器的内部数据结构是简单的，每个字节码只需要几个本机机器指令即可实现。解释器体积小，可以很容易确定评估表达式所需的内存和时间的严格限制，使其适用于实时应用程序中的调试代理。

---


• [General Bytecode Design](General-Bytecode-Design.html#General-Bytecode-Design):                    Overview of the interpreter.

> • [通用字节码设计](General-Bytecode-Design.html#General-Bytecode-Design):                概述解释器。

• [Bytecode Descriptions](Bytecode-Descriptions.html#Bytecode-Descriptions):                          What each one does.

> • [字节码描述](Bytecode-Descriptions.html#Bytecode-Descriptions): 每个字节码的作用。

• [Using Agent Expressions](Using-Agent-Expressions.html#Using-Agent-Expressions):                    How agent expressions fit into the big picture.

> • [使用代理表达式](Using-Agent-Expressions.html#Using-Agent-Expressions):  如何将代理表达式置于大局之中。

• [Varying Target Capabilities](Varying-Target-Capabilities.html#Varying-Target-Capabilities):        How to discover what the target can do.

> •[可变的目标功能](Varying-Target-Capabilities.html#Varying-Target-Capabilities):  如何发现目标可以做什么。

• [Rationale](Rationale.html#Rationale):                                                              Why we did it this way.

> • [理由](Rationale.html#Rationale):  为什么我们这样做。

---

---

::: header
Next: [Target Descriptions](Target-Descriptions.html#Target-Descriptions)]
:::
