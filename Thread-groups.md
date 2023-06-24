---
tip: translate by openai@2023-06-24 03:53:42
...
---
description: Thread groups (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Thread groups (Debugging with GDB)
lang: en
resource-type: document
title: Thread groups (Debugging with GDB)
---
::: header
Previous: [Asynchronous and non-stop modes](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes)]
:::

---

#### 27.1.3 Thread groups


[GDB] may support debugging of several hardware systems, each one having several cores with several different processes running on each core. This section describes the MI mechanism to support such debugging scenarios.

> [GDB] 可以支持调试多个硬件系统，每个系统都有多个核心，每个核心上运行着多个不同的进程。本节将介绍 MI 机制来支持这种调试场景。


The key observation is that regardless of the structure of the target, MI can have a global list of threads, because most commands that accept the '`--thread`' option, nor an notion of the current process in the MI interface. The only strictly new feature that is required is the ability to find how the threads are grouped into processes.

> 观察到的关键是，无论目标的结构如何，MI都可以有一个全局的线程列表，因为大多数接受'--thread'选项的命令，在MI界面中都没有当前进程的概念。唯一需要的严格新特性是能够找到如何将线程分组成进程。


To allow the user to discover such grouping, and to support arbitrary hierarchy of machines/cores/processes, MI introduces the concept of a *thread group*. Thread group is a collection of threads and other thread groups. A thread group always has a string identifier, a type, and may have additional attributes specific to the type. A new command, `-list-thread-groups`, returns the list of top-level thread groups, which correspond to processes that [GDB] is debugging at the moment. By passing an identifier of a thread group to the `-list-thread-groups` command, it is possible to obtain the members of specific thread group.

> 为了让用户发现这种分组，并支持机器/核心/进程的任意层次结构，MI引入了线程组的概念。线程组是一组线程和其他线程组的集合。线程组总是具有字符串标识符、类型，并且可能具有与类型相关的其他属性。新命令`-list-thread-groups`返回顶级线程组的列表，这些线程组对应于[GDB]当前正在调试的进程。通过将线程组的标识符传递给`-list-thread-groups`命令，可以获得特定线程组的成员。


To allow the user to easily discover processes, and other objects, he wishes to debug, a concept of *available thread group* is introduced. Available thread group is an thread group that [GDB]'. In general, the content of a thread group may be only retrieved only after attaching to that thread group.

> 为了让用户可以轻松发现他想要调试的进程和其他对象，引入了*可用线程组*的概念。可用线程组是一个[GDB]的线程组。通常只有在附加到该线程组之后，才能检索线程组的内容。


Thread groups are related to inferiors (see [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)). Each inferior corresponds to a thread group of a special type '`process`', and some additional operations are permitted on such thread groups.

> 线程组与下属（参见[下属连接和程序]（Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs））有关。每个下属对应于一个特殊类型的线程组'`process`'，并且允许在这样的线程组上执行一些额外的操作。

---

::: header
Previous: [Asynchronous and non-stop modes](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes)]
:::
