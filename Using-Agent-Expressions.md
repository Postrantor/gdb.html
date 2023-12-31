---
tip: translate by openai@2023-06-24 04:32:16
...
---
description: Using Agent Expressions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Using Agent Expressions (Debugging with GDB)
lang: en
resource-type: document
title: Using Agent Expressions (Debugging with GDB)
---
::: header
Next: [Varying Target Capabilities](Varying-Target-Capabilities.html#Varying-Target-Capabilities)]
:::

---

### F.3 Using Agent Expressions


Agent expressions can be used in several different ways by [GDB], and the debugger can generate different bytecode sequences as appropriate.

> 代理表达式可以被[GDB]用于多种不同的方式，调试器可以根据需要生成不同的字节码序列。


One possibility is to do expression evaluation on the target rather than the host, such as for the conditional of a conditional tracepoint. In such a case, [GDB] compiles the source expression into a bytecode sequence that simply gets values from registers or memory, does arithmetic, and returns a result.

> 一种可能性是在目标上而不是主机上进行表达式求值，比如对于条件断点的条件。在这种情况下，[GDB]将源表达式编译为字节码序列，它仅从寄存器或内存中获取值，执行算术运算，并返回结果。


Another way to use agent expressions is for tracepoint data collection. [GDB] adds `trace` bytecodes to save the pieces of memory that were used.

> 另一种使用代理表达式的方法是用于跟踪点数据收集。[GDB]添加了`跟踪`字节码来保存所使用的内存片段。

- The user selects trace points in the program's code at which GDB should collect data.

- The user specifies expressions to evaluate at each trace point. These expressions may denote objects in memory, in which case those objects' contents are recorded as the program runs, or computed values, in which case the values themselves are recorded.

> 用户在每个跟踪点指定要计算的表达式。如果这些表达式代表内存中的对象，则会记录程序运行时对象的内容；如果是计算值，则会记录值本身。

- GDB transmits the tracepoints and their associated expressions to the GDB agent, running on the debugging target.

> GDB将断点和相关表达式传输到在调试目标上运行的GDB代理。
- The agent arranges to be notified when a trace point is hit.

- When execution on the target reaches a trace point, the agent evaluates the expressions associated with that trace point, and records the resulting values and memory ranges.

> 当在目标上执行到跟踪点时，代理会评估与该跟踪点相关联的表达式，并记录产生的值和内存范围。

- Later, when the user selects a given trace event and inspects the objects and expression values recorded, GDB talks to the agent to retrieve recorded data as necessary to meet the user's requests. If the user asks to see an object whose contents have not been recorded, GDB reports an error.

> 当用户选择给定的跟踪事件并检查记录的对象和表达式值时，GDB与代理进行通信以检索所需的记录数据，以满足用户的请求。如果用户要查看尚未记录的对象，GDB将报告错误。

---

::: header
Next: [Varying Target Capabilities](Varying-Target-Capabilities.html#Varying-Target-Capabilities)]
:::
