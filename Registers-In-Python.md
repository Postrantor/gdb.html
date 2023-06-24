---
tip: translate by openai@2023-06-24 02:00:17
...
---
description: Registers In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Registers In Python (Debugging with GDB)
lang: en
resource-type: document
title: Registers In Python (Debugging with GDB)
---
::: header
Next: [Connections In Python](Connections-In-Python.html#Connections-In-Python)]
:::

---

#### 23.3.2.35 Registers In Python


Python code can request from a `gdb.Architecture` information about the set of registers available (see [`Architecture.registers`](Architectures-In-Python.html#gdbpy_005farchitecture_005fregisters)). The register information is returned as a `gdb.RegisterDescriptorIterator`, which is an iterator that in turn returns `gdb.RegisterDescriptor` objects.

> Python代码可以从`gdb.Architecture`中请求关于可用寄存器集的信息（参见[`Architecture.registers`](Architectures-In-Python.html#gdbpy_005farchitecture_005fregisters)）。寄存器信息作为`gdb.RegisterDescriptorIterator`返回，它是一个迭代器，又返回`gdb.RegisterDescriptor`对象。


A `gdb.RegisterDescriptor` does not provide the value of a register (see [`Frame.read_register`](Frames-In-Python.html#gdbpy_005fframe_005fread_005fregister) for reading a register's value), instead the `RegisterDescriptor` is a way to discover which registers are available for a particular architecture.

> `gdb.RegisterDescriptor`不提供寄存器的值（参见[`Frame.read_register`]（Frames-In-Python.html#gdbpy_005fframe_005fread_005fregister）以读取寄存器的值），而是一种发现特定架构可用寄存器的方式。

A `gdb.RegisterDescriptor` has the following read-only properties:

Variable: **RegisterDescriptor.name**

:   The name of this register.


It is also possible to lookup a register descriptor based on its name using the following `gdb.RegisterDescriptorIterator` function:

> 可以使用以下`gdb.RegisterDescriptorIterator`函数基于其名称查找寄存器描述符：

Function: **RegisterDescriptorIterator.find** *(name)*


:   Takes `name` as an argument, which must be a string, and returns a `gdb.RegisterDescriptor` for the register with that name, or `None` if there is no register with that name.

> 接受`name`作为参数，它必须是一个字符串，并返回一个`gdb.RegisterDescriptor`，用于具有该名称的寄存器，如果没有具有该名称的寄存器则返回`None`。


Python code can also request from a `gdb.Architecture` information about the set of register groups available on a given architecture (see [`Architecture.register_groups`](Architectures-In-Python.html#gdbpy_005farchitecture_005freggroups)).

> Python 代码也可以从`gdb.Architecture`请求有关给定架构上可用的寄存器组集的信息（请参阅[`Architecture.register_groups`](Architectures-In-Python.html#gdbpy_005farchitecture_005freggroups)）。


Every register can be a member of zero or more register groups. Some register groups are used internally within [GDB] to control things like which registers must be saved when calling into the program being debugged (see [Calling Program Functions](Calling.html#Calling)). Other register groups exist to allow users to easily see related sets of registers in commands like `info registers` (see [`info registers reggroup`](Registers.html#info_005fregisters_005freggroup)).

> 每个寄存器可以属于零个或多个寄存器组。有些寄存器组是用于在[GDB]内部控制调用被调试程序时必须保存哪些寄存器（参见[调用程序函数](Calling.html#Calling))。其他寄存器组可以让用户在像`info registers`这样的命令中轻松查看相关的寄存器集（参见[`info registers reggroup`](Registers.html#info_005fregisters_005freggroup)）。


The register groups information is returned as a `gdb.RegisterGroupsIterator`, which is an iterator that in turn returns `gdb.RegisterGroup` objects.

> 返回的寄存器组信息作为`gdb.RegisterGroupsIterator`返回，这是一个迭代器，又返回`gdb.RegisterGroup`对象。

A `gdb.RegisterGroup` object has the following read-only properties:

Variable: **RegisterGroup.name**

:   A string that is the name of this register group.

---

::: header
Next: [Connections In Python](Connections-In-Python.html#Connections-In-Python)]
:::
