---
tip: translate by openai@2023-06-23 17:17:50
...
---
description: Annotations (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Annotations (Debugging with GDB)
lang: en
resource-type: document
title: Annotations (Debugging with GDB)
---
::: header
Next: [Debugger Adapter Protocol](Debugger-Adapter-Protocol.html#Debugger-Adapter-Protocol)]
:::

---

## 28 [GDB]


This chapter describes annotations in [GDB] at a relatively high level.

> 本章介绍了[GDB]中的注释，以较高的水平。


The annotation mechanism has largely been superseded by [GDB/MI] (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)).

> 注释机制已经大部分被[GDB/MI]（参见[GDB/MI](GDB_002fMI.html#GDB_002fMI)）所取代。

---


• [Annotations Overview](Annotations-Overview.html#Annotations-Overview):                 What annotations are; the general syntax.

> • [注释概览](Annotations-Overview.html#Annotations-Overview): 什么是注释；一般语法。

• [Server Prefix](Server-Prefix.html#Server-Prefix):                                      Issuing a command without affecting user state.

> • [服务器前缀](Server-Prefix.html#Server-Prefix):  不影响用户状态的发出命令。

• [Prompting](Prompting.html#Prompting)'s need for input.

> • 需要输入的提示（Prompting）。

• [Errors](Errors.html#Errors):                                                           Annotations for error messages.

> • [错误](Errors.html#Errors)：错误消息的注释。

• [Invalidation](Invalidation.html#Invalidation):                                         Some annotations describe things now invalid.

> • [无效化](Invalidation.html#Invalidation)：有些注释描述的事情现在已经无效。

• [Annotations for Running](Annotations-for-Running.html#Annotations-for-Running):        Whether the program is running, how it stopped, etc.

> • [运行注释](Annotations-for-Running.html#Annotations-for-Running):        程序是否正在运行，它是如何停止的等等。

• [Source Annotations](Source-Annotations.html#Source-Annotations):                       Annotations describing source code.

> • [源注释](Source-Annotations.html#Source-Annotations)：注释描述源代码。

---
