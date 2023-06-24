---
tip: translate by openai@2023-06-24 03:50:19
...
---
description: Targets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Targets (Debugging with GDB)
lang: en
resource-type: document
title: Targets (Debugging with GDB)
---
::: header
Next: [Remote Debugging](Remote-Debugging.html#Remote-Debugging)]
:::

---

## 19 Specifying a Debugging Target

A *target* is the execution environment occupied by your program.


Often, [GDB] (see [Commands for Managing Targets](Target-Commands.html#Target-Commands)).

> 经常使用GDB（参见[目标管理命令](Target-Commands.html#Target-Commands)）。

It is possible to build [GDB] command.

`set architecture arch`


This command sets the current target architecture to `arch` can be `"auto"`, in addition to one of the supported architectures.

> 这个命令将当前目标架构设置为`arch`，可以是`"auto"`，除此之外还支持其他架构。

`show architecture`

Show the current target architecture.

`set processor`

`processor`


These are alias commands for, respectively, `set architecture` and `show architecture`.

> 这些分别是 `设置架构` 和 `显示架构` 的别名命令。

---


• [Active Targets](Active-Targets.html#Active-Targets):           Active targets

> • [有效目标](Active-Targets.html#Active-Targets): 有效目标

• [Target Commands](Target-Commands.html#Target-Commands):        Commands for managing targets

> • [目标命令](Target-Commands.html#Target-Commands):       用于管理目标的命令

• [Byte Order](Byte-Order.html#Byte-Order):                       Choosing target byte order

> • [字节顺序](Byte-Order.html#Byte-Order)：选择目标字节顺序

---
