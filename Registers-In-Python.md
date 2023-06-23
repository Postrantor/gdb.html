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

A `gdb.RegisterDescriptor` does not provide the value of a register (see [`Frame.read_register`](Frames-In-Python.html#gdbpy_005fframe_005fread_005fregister) for reading a register's value), instead the `RegisterDescriptor` is a way to discover which registers are available for a particular architecture.

A `gdb.RegisterDescriptor` has the following read-only properties:

Variable: **RegisterDescriptor.name**

:   The name of this register.

It is also possible to lookup a register descriptor based on its name using the following `gdb.RegisterDescriptorIterator` function:

Function: **RegisterDescriptorIterator.find** *(name)*

:   Takes `name` as an argument, which must be a string, and returns a `gdb.RegisterDescriptor` for the register with that name, or `None` if there is no register with that name.

Python code can also request from a `gdb.Architecture` information about the set of register groups available on a given architecture (see [`Architecture.register_groups`](Architectures-In-Python.html#gdbpy_005farchitecture_005freggroups)).

Every register can be a member of zero or more register groups. Some register groups are used internally within [GDB] to control things like which registers must be saved when calling into the program being debugged (see [Calling Program Functions](Calling.html#Calling)). Other register groups exist to allow users to easily see related sets of registers in commands like `info registers` (see [`info registers reggroup`](Registers.html#info_005fregisters_005freggroup)).

The register groups information is returned as a `gdb.RegisterGroupsIterator`, which is an iterator that in turn returns `gdb.RegisterGroup` objects.

A `gdb.RegisterGroup` object has the following read-only properties:

Variable: **RegisterGroup.name**

:   A string that is the name of this register group.

---

::: header
Next: [Connections In Python](Connections-In-Python.html#Connections-In-Python)]
:::
