---
tip: translate by openai@2023-06-23 23:40:00
...
---
description: IPA Protocol Objects (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: IPA Protocol Objects (Debugging with GDB)
lang: en
resource-type: document
title: IPA Protocol Objects (Debugging with GDB)
---
::: header
Next: [IPA Protocol Commands](IPA-Protocol-Commands.html#IPA-Protocol-Commands)]
:::

---

#### 31.1.1 IPA Protocol Objects


The commands sent to and results received from agent may contain some complex data types called *objects*.

> 命令发送到代理机和接收到的结果可能包含一些称为*对象*的复杂数据类型。


The in-process agent is running on the same machine with [GDB] or GDBserver, so it doesn't have to handle as much differences between two ends as remote protocol (see [Remote Protocol](Remote-Protocol.html#Remote-Protocol)) tries to handle. However, there are still some differences of two ends in two processes:

> 在进程代理运行在同一台机器上的[GDB]或GDBserver，因此它不必处理远程协议（参见[远程协议]（Remote-Protocol.html#Remote-Protocol））尝试处理的两端之间的差异。但是，两个进程中仍有一些差异：


1. word size. On some 64-bit machines, [GDB] or GDBserver can be compiled as a 64-bit executable, while in-process agent is a 32-bit one.

> 在某些64位机器上，[GDB]或GDBserver可以编译为64位可执行文件，而内部代理则是32位的。

2. ABI. Some machines may have multiple types of ABI, [GDB] or GDBserver is compiled with one, and in-process agent is compiled with the other one.

> 2. ABI。有些机器可能有多种ABI，[GDB]或GDBserver编译为一种，而内部进程代理则编译为另一种。

Here are the IPA Protocol Objects:


1. agent expression object. It represents an agent expression (see [Agent Expressions](Agent-Expressions.html#Agent-Expressions)).

> 1. 代理表达式对象。它代表一个代理表达式（参见[代理表达式] (Agent-Expressions.html#Agent-Expressions)）。

2. tracepoint action object. It represents a tracepoint action (see [Tracepoint Action Lists](Tracepoint-Actions.html#Tracepoint-Actions)) to collect registers, memory, static trace data and to evaluate expression.

> 2. 跟踪点动作对象。它代表一个跟踪点动作（参见[跟踪点动作列表](Tracepoint-Actions.html#Tracepoint-Actions))来收集寄存器、内存、静态跟踪数据，并评估表达式。

3. tracepoint object. It represents a tracepoint (see [Tracepoints](Tracepoints.html#Tracepoints)).

> 3. 跟踪点对象。它表示一个跟踪点（参见[跟踪点](Tracepoints.html#Tracepoints)）。


The following table describes important attributes of each IPA protocol object:

> 以下表格描述了每个IPA协议对象的重要属性：


Name                                                   Size                                                                                             Description

> 名称                                                   大小                                                                                             描述

---

*agent expression object*

length                                                 4                                                                                                length of bytes code

> 长度为4个字节的代码

byte code                                              `length`                                                                              contents of byte code

> 字节码：长度：字节码的内容
*tracepoint action for collecting memory*

'M'                                                    1                                                                                                type of tracepoint action

> 'M' 是一种跟踪点动作的类型。

addr                                                   8                                                                                                if `basereg` for memory collecting.

> 如果“basereg”用于内存收集，addr 8。

len                                                    8                                                                                                length of memory for collecting

> 内存收集的长度为8。

basereg                                                4                                                                                                the register number containing the starting memory address for collecting.

> 这个寄存器号包含用于收集的起始内存地址。
*tracepoint action for collecting registers*

'R'                                                    1                                                                                                type of tracepoint action

> 'R'是一种跟踪点动作的类型。
*tracepoint action for collecting static trace data*

'L'                                                    1                                                                                                type of tracepoint action

> 'L' 是跟踪点动作的一种类型。
*tracepoint action for expression evaluation*

'X'                                                    1                                                                                                type of tracepoint action

> 'X'是一种跟踪点动作的类型。

agent expression                                       length of                                                                                        [agent expression object](#agent-expression-object)

> 代理表达的长度
*tracepoint object*

number                                                 4                                                                                                number of tracepoint

> 数字4，跟踪点的数量

address                                                8                                                                                                address of tracepoint inserted on

> 地址：插入的跟踪点的地址 8

type                                                   4                                                                                                type of tracepoint

> 类型4是跟踪点的类型。

enabled                                                1                                                                                                enable or disable of tracepoint

> 启用跟踪点的启用或禁用

step_count                                             8                                                                                                step

> 步数：8步

pass_count                                             8                                                                                                pass

> 通过计数： 8 次

numactions                                             4                                                                                                number of tracepoint actions

> 数量行动：4，跟踪点行动的数量

hit count                                              8                                                                                                hit count

> 点击次数 8

trace frame usage                                      8                                                                                                trace frame usage

> 追踪帧使用情况

compiled_cond                                          8                                                                                                compiled condition

> 编译条件：雇佣 8 人
orig_size                                              8                                                                                                orig size

condition                                              4 if condition is NULL otherwise length of [agent expression object](#agent-expression-object)   zero if condition is NULL, otherwise is [agent expression object](#agent-expression-object)

> 如果条件为空，则为零，否则为[代理表达式对象](#agent-expression-object)的长度。

actions                                                variable                                                                                         numactions number of [tracepoint action object](#tracepoint-action-object)

> 行动变量numactions表示[跟踪点行动对象](#tracepoint-action-object)的数量。

---

::: header
Next: [IPA Protocol Commands](IPA-Protocol-Commands.html#IPA-Protocol-Commands)]
:::
