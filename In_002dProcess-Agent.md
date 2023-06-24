---
tip: translate by openai@2023-06-23 23:38:22
...
---
description: In-Process Agent (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: In-Process Agent (Debugging with GDB)
lang: en
resource-type: document
title: In-Process Agent (Debugging with GDB)
---
::: header
Next: [GDB Bugs](GDB-Bugs.html#GDB-Bugs)]
:::

---

## 31 In-Process Agent


The traditional debugging model is conceptually low-speed, but works fine, because most bugs can be reproduced in debugging-mode execution. However, as multi-core or many-core processors are becoming mainstream, and multi-threaded programs become more and more popular, there should be more and more bugs that only manifest themselves at normal-mode execution, for example, thread races, because debugger's interference with the program's timing may conceal the bugs. On the other hand, in some applications, it is not feasible for the debugger to interrupt the program's execution long enough for the developer to learn anything helpful about its behavior. If the program's correctness depends on its real-time behavior, delays introduced by a debugger might cause the program to fail, even when the code itself is correct. It is useful to be able to observe the program's behavior without interrupting it.

> 传统的调试模型在概念上速度较慢，但是表现良好，因为大多数错误都能在调试模式下重现。然而，随着多核或多核处理器变得越来越普及，多线程程序变得越来越流行，应该会有越来越多的错误只在正常模式下才能表现出来，例如线程竞争，因为调试器对程序的时间干扰可能会掩盖这些错误。另一方面，在某些应用中，调试器不可能中断程序的执行时间足够长，以便开发者能够了解有用的信息。如果程序的正确性取决于它的实时行为，调试器引入的延迟可能会导致程序失败，即使代码本身是正确的。有时可以观察程序的行为而不中断它是很有用的。


Therefore, traditional debugging model is too intrusive to reproduce some bugs. In order to reduce the interference with the program, we can reduce the number of operations performed by debugger. The *In-Process Agent*, a shared library, is running within the same process with inferior, and is able to perform some debugging operations itself. As a result, debugger is only involved when necessary, and performance of debugging can be improved accordingly. Note that interference with program can be reduced but can't be removed completely, because the in-process agent will still stop or slow down the program.

> 因此，传统的调试模型太过侵入性，无法重现某些错误。为了减少对程序的干扰，我们可以减少调试器执行的操作数量。*In-Process Agent*是一个共享库，运行在与inferior相同的进程中，能够自行执行一些调试操作。因此，只有在必要时才会涉及调试器，调试性能可以相应地提高。请注意，可以减少对程序的干扰，但无法完全消除，因为in-process agent仍会暂停或减慢程序的执行。


The in-process agent can interpret and execute Agent Expressions (see [Agent Expressions](Agent-Expressions.html#Agent-Expressions)) during performing debugging operations. The agent expressions can be used for different purposes, such as collecting data in tracepoints, and condition evaluation in breakpoints.

> 代理程序可以在执行调试操作时解释和执行代理表达式（参见[代理表达式](Agent-Expressions.html#Agent-Expressions))。代理表达式可以用于不同的目的，例如在断点中收集数据和条件评估。


You can control whether the in-process agent is used as an aid for debugging with the following commands:

> 您可以使用以下命令控制是否使用内置代理作为调试辅助工具：

`set agent on`


Causes the in-process agent to perform some operations on behalf of the debugger. Just which operations requested by the user will be done by the in-process agent depends on the its capabilities. For example, if you request to evaluate breakpoint conditions in the in-process agent, and the in-process agent has such capability as well, then breakpoint conditions will be evaluated in the in-process agent.

> 让内部进程代理为调试器执行一些操作。由用户请求的哪些操作将由内部进程代理完成取决于其能力。例如，如果您请求在内部进程代理中评估断点条件，而内部进程代理也具有此功能，则断点条件将在内部进程代理中评估。

`set agent off`


Disables execution of debugging operations by the in-process agent. All of the operations will be performed by [GDB].

> 禁用进程代理的调试操作执行。所有操作将由[GDB]执行。

`show agent`


Display the current setting of execution of debugging operations by the in-process agent.

> 顯示由內部處理代理執行除錯操作的當前設定。

---


• [In-Process Agent Protocol](In_002dProcess-Agent-Protocol.html#In_002dProcess-Agent-Protocol):     

> • [In-Process Agent Protocol](In_002dProcess-Agent-Protocol.html#In_002dProcess-Agent-Protocol): 
  进程代理协议

---

---

::: header
Next: [GDB Bugs](GDB-Bugs.html#GDB-Bugs)]
:::
