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

The in-process agent is running on the same machine with [GDB] or GDBserver, so it doesn't have to handle as much differences between two ends as remote protocol (see [Remote Protocol](Remote-Protocol.html#Remote-Protocol)) tries to handle. However, there are still some differences of two ends in two processes:

1. word size. On some 64-bit machines, [GDB] or GDBserver can be compiled as a 64-bit executable, while in-process agent is a 32-bit one.
2. ABI. Some machines may have multiple types of ABI, [GDB] or GDBserver is compiled with one, and in-process agent is compiled with the other one.

Here are the IPA Protocol Objects:

1. agent expression object. It represents an agent expression (see [Agent Expressions](Agent-Expressions.html#Agent-Expressions)).
2. tracepoint action object. It represents a tracepoint action (see [Tracepoint Action Lists](Tracepoint-Actions.html#Tracepoint-Actions)) to collect registers, memory, static trace data and to evaluate expression.
3. tracepoint object. It represents a tracepoint (see [Tracepoints](Tracepoints.html#Tracepoints)).

The following table describes important attributes of each IPA protocol object:

Name                                                   Size                                                                                             Description

---

*agent expression object*
length                                                 4                                                                                                length of bytes code
byte code                                              `length`                                                                              contents of byte code
*tracepoint action for collecting memory*
'M'                                                    1                                                                                                type of tracepoint action
addr                                                   8                                                                                                if `basereg` for memory collecting.
len                                                    8                                                                                                length of memory for collecting
basereg                                                4                                                                                                the register number containing the starting memory address for collecting.
*tracepoint action for collecting registers*
'R'                                                    1                                                                                                type of tracepoint action
*tracepoint action for collecting static trace data*
'L'                                                    1                                                                                                type of tracepoint action
*tracepoint action for expression evaluation*
'X'                                                    1                                                                                                type of tracepoint action
agent expression                                       length of                                                                                        [agent expression object](#agent-expression-object)
*tracepoint object*
number                                                 4                                                                                                number of tracepoint
address                                                8                                                                                                address of tracepoint inserted on
type                                                   4                                                                                                type of tracepoint
enabled                                                1                                                                                                enable or disable of tracepoint
step_count                                             8                                                                                                step
pass_count                                             8                                                                                                pass
numactions                                             4                                                                                                number of tracepoint actions
hit count                                              8                                                                                                hit count
trace frame usage                                      8                                                                                                trace frame usage
compiled_cond                                          8                                                                                                compiled condition
orig_size                                              8                                                                                                orig size
condition                                              4 if condition is NULL otherwise length of [agent expression object](#agent-expression-object)   zero if condition is NULL, otherwise is [agent expression object](#agent-expression-object)
actions                                                variable                                                                                         numactions number of [tracepoint action object](#tracepoint-action-object)

---

::: header
Next: [IPA Protocol Commands](IPA-Protocol-Commands.html#IPA-Protocol-Commands)]
:::
