---
tip: translate by openai@2023-06-23 21:59:04
...
---
description: GDB/MI Frame Information (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Frame Information (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Frame Information (Debugging with GDB)
---
::: header
Next: [GDB/MI Thread Information](GDB_002fMI-Thread-Information.html#GDB_002fMI-Thread-Information)]
:::

---

#### 27.5.5 [GDB/MI]


Response from many MI commands includes an information about stack frame. This information is a tuple that may have the following fields:

> 许多MI命令的响应包括有关堆栈帧的信息。此信息是一个元组，可能具有以下字段：

`level`


:   The level of the stack frame. The innermost frame has the level of zero. This field is always present.

> 栈帧的级别。最内层的帧具有零级。这个字段总是存在的。

`func`


:   The name of the function corresponding to the frame. This field may be absent if [GDB] is unable to determine the function name.

> 函数名称与帧对应。如果[GDB]无法确定函数名称，此字段可能会缺失。

`addr`

:   The code address for the frame. This field is always present.

`addr_flags`


:   Optional field containing any flags related to the address. These flags are architecture-dependent; see [Architectures](Architectures.html#Architectures) for their meaning for a particular CPU.

> 可选字段，包含与地址相关的任何标志。这些标志是与体系结构相关的；查看[架构](Architectures.html#Architectures) 了解它们对特定CPU的含义。

`file`


:   The name of the source files that correspond to the frame's code address. This field may be absent.

> 这个字段可能不存在，它对应于帧代码地址的源文件的名称。

`line`


:   The source line corresponding to the frames' code address. This field may be absent.

> 对应帧代码地址的源代码行。此字段可能会缺失。

`from`


:   The name of the binary file (either executable or shared library) the corresponds to the frame's code address. This field may be absent.

> 此帧代码地址对应的二进制文件（可执行文件或共享库）的名称。此字段可能不存在。
