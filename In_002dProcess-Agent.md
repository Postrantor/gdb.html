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

Therefore, traditional debugging model is too intrusive to reproduce some bugs. In order to reduce the interference with the program, we can reduce the number of operations performed by debugger. The *In-Process Agent*, a shared library, is running within the same process with inferior, and is able to perform some debugging operations itself. As a result, debugger is only involved when necessary, and performance of debugging can be improved accordingly. Note that interference with program can be reduced but can't be removed completely, because the in-process agent will still stop or slow down the program.

The in-process agent can interpret and execute Agent Expressions (see [Agent Expressions](Agent-Expressions.html#Agent-Expressions)) during performing debugging operations. The agent expressions can be used for different purposes, such as collecting data in tracepoints, and condition evaluation in breakpoints.

You can control whether the in-process agent is used as an aid for debugging with the following commands:

`set agent on`

Causes the in-process agent to perform some operations on behalf of the debugger. Just which operations requested by the user will be done by the in-process agent depends on the its capabilities. For example, if you request to evaluate breakpoint conditions in the in-process agent, and the in-process agent has such capability as well, then breakpoint conditions will be evaluated in the in-process agent.

`set agent off`

Disables execution of debugging operations by the in-process agent. All of the operations will be performed by [GDB].

`show agent`

Display the current setting of execution of debugging operations by the in-process agent.

---

• [In-Process Agent Protocol](In_002dProcess-Agent-Protocol.html#In_002dProcess-Agent-Protocol):     

---

---

::: header
Next: [GDB Bugs](GDB-Bugs.html#GDB-Bugs)]
:::
