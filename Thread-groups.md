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

The key observation is that regardless of the structure of the target, MI can have a global list of threads, because most commands that accept the '`--thread`' option, nor an notion of the current process in the MI interface. The only strictly new feature that is required is the ability to find how the threads are grouped into processes.

To allow the user to discover such grouping, and to support arbitrary hierarchy of machines/cores/processes, MI introduces the concept of a *thread group*. Thread group is a collection of threads and other thread groups. A thread group always has a string identifier, a type, and may have additional attributes specific to the type. A new command, `-list-thread-groups`, returns the list of top-level thread groups, which correspond to processes that [GDB] is debugging at the moment. By passing an identifier of a thread group to the `-list-thread-groups` command, it is possible to obtain the members of specific thread group.

To allow the user to easily discover processes, and other objects, he wishes to debug, a concept of *available thread group* is introduced. Available thread group is an thread group that [GDB]'. In general, the content of a thread group may be only retrieved only after attaching to that thread group.

Thread groups are related to inferiors (see [Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)). Each inferior corresponds to a thread group of a special type '`process`', and some additional operations are permitted on such thread groups.

---

::: header
Previous: [Asynchronous and non-stop modes](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes)]
:::
