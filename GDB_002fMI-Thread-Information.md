---
tip: translate by openai@2023-06-23 22:19:45
...
---
description: GDB/MI Thread Information (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Thread Information (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Thread Information (Debugging with GDB)
---
::: header
Next: [GDB/MI Ada Exception Information](GDB_002fMI-Ada-Exception-Information.html#GDB_002fMI-Ada-Exception-Information)]
:::

---

#### 27.5.6 [GDB/MI]


Whenever [GDB] has to report an information about a thread, it uses a tuple with the following fields. The fields are always present unless stated otherwise.

> 每当GDB需要报告关于线程的信息时，它都会使用一个元组，其中包含以下字段。除非另有说明，否则这些字段总是存在的。

`id`

:   The global numeric id assigned to the thread by [GDB].

`target-id`

:   The target-specific string identifying the thread.

`details`


:   Additional information about the thread provided by the target. It is supposed to be human-readable and not interpreted by the frontend. This field is optional.

> 针对目标提供的有关线程的附加信息。它应该是可读的，而不是由前端解释的。此字段是可选的。

`name`


:   The name of the thread. If the user specified a name using the `thread name` command, then this name is given. Otherwise, if [GDB] cannot find the thread name, then this field is omitted.

> 线程的名称。如果用户使用“线程名”命令指定了名称，则给出该名称。否则，如果[GDB]找不到线程名，则省略此字段。

`state`


:   The execution state of the thread, either '`stopped`', depending on whether the thread is presently running.

> 线程的执行状态，要么是“停止”，要么取决于线程当前是否正在运行。

`frame`


:   The stack frame currently executing in the thread. This field is only present if the thread is stopped. Its format is documented in [GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information).

> 当前在线程中正在执行的堆栈帧。如果线程停止，此字段才会出现。其格式可参见[GDB/MI Frame Information](GDB_002fMI-Frame-Information.html#GDB_002fMI-Frame-Information)文档。

`core`


:   The value of this field is an integer number of the processor core the thread was last seen on. This field is optional.

> 这个字段的值是线程最后被发现所在处理器核心的整数。此字段是可选的。
