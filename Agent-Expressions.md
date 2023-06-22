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

Using GDB's `trace` and `collect` commands, the user can specify locations in the program, and arbitrary expressions to evaluate when those locations are reached. Later, using the `tfind` command, she can examine the values those expressions had when the program hit the trace points. The expressions may also denote objects in memory --- structures or arrays, for example --- whose values GDB should record; while visiting a particular tracepoint, the user may inspect those objects as if they were in memory at that moment. However, because GDB records these values without interacting with the user, it can do so quickly and unobtrusively, hopefully not disturbing the program's behavior.

When GDB is debugging a remote target, the GDB *agent* code running on the target computes the values of the expressions itself. To avoid having a full symbolic expression evaluator on the agent, GDB translates expressions in the source language into a simpler bytecode language, and then sends the bytecode to the agent; the agent then executes the bytecode, and records the values for GDB to retrieve later.

The bytecode language is simple; there are forty-odd opcodes, the bulk of which are the usual vocabulary of C operands (addition, subtraction, shifts, and so on) and various sizes of literals and memory reference operations. The bytecode interpreter operates strictly on machine-level values --- various sizes of integers and floating point numbers --- and requires no information about types or symbols; thus, the interpreter's internal data structures are simple, and each bytecode requires only a few native machine instructions to implement it. The interpreter is small, and strict limits on the memory and time required to evaluate an expression are easy to determine, making it suitable for use by the debugging agent in real-time applications.

---

• [General Bytecode Design](General-Bytecode-Design.html#General-Bytecode-Design):                    Overview of the interpreter.
• [Bytecode Descriptions](Bytecode-Descriptions.html#Bytecode-Descriptions):                          What each one does.
• [Using Agent Expressions](Using-Agent-Expressions.html#Using-Agent-Expressions):                    How agent expressions fit into the big picture.
• [Varying Target Capabilities](Varying-Target-Capabilities.html#Varying-Target-Capabilities):        How to discover what the target can do.
• [Rationale](Rationale.html#Rationale):                                                              Why we did it this way.

---

---

::: header
Next: [Target Descriptions](Target-Descriptions.html#Target-Descriptions)]
:::
