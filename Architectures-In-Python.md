---
tip: translate by openai@2023-06-23 17:24:12
...
---
description: Architectures In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Architectures In Python (Debugging with GDB)
lang: en
resource-type: document
title: Architectures In Python (Debugging with GDB)
---
::: header
Next: [Registers In Python](Registers-In-Python.html#Registers-In-Python)]
:::

---

#### 23.3.2.34 Python representation of architectures


[GDB] uses architecture specific parameters and artifacts in a number of its various computations. An architecture is represented by an instance of the `gdb.Architecture` class.

> GDB在其各种计算中使用特定于架构的参数和工件。一种架构由gdb.Architecture类的实例表示。


A `gdb.Architecture` class has the following methods:

> `gdb.Architecture`类具有以下方法：


Function: **Architecture.name** *()*

> 功能：**Architecture.name** *（）*


:   Return the name (string value) of the architecture.

> 返回架构的名称（字符串值）。

```
<!-- -->
```

)*


:   Return a list of disassembled instructions starting from the memory address `start_pc` is returned. For all of these cases, each element of the returned list is a Python `dict` with the following string keys:

> 返回从内存地址'start_pc'开始的拆解指令列表。 对于所有这些情况，返回的列表的每个元素都是一个具有以下字符串键的Python 'dict'：

```
`addr`

:   The value corresponding to this key is a Python long integer capturing the memory address of the instruction.

`asm`

:   The value corresponding to this key is a string value which represents the instruction with assembly language mnemonics. The assembly language flavor used is the same as that specified by the current CLI variable `disassembly-flavor`. See [Machine Code](Machine-Code.html#Machine-Code).

`length`

:   The value corresponding to this key is the length (integer value) of the instruction in bytes.
```

)*


:   This function looks up an integer type by its `size`, and optionally whether or not it is signed.

> 这个函数通过它的“大小”查找整数类型，并可选择是否有符号。

```
`size` is the size, in bits, of the desired integer type. Only certain sizes are currently supported: 0, 8, 16, 24, 32, 64, and 128.

If `signed` is `False`, the returned type will be unsigned.

If the indicated type cannot be found, this function will throw a `ValueError` exception.
```

)*


:   Return a `gdb.RegisterDescriptorIterator` (see [Registers In Python](Registers-In-Python.html#Registers-In-Python)) for all of the registers in `reggroup`' is assumed.

> 返回一个`gdb.RegisterDescriptorIterator`（参见[Python中的寄存器](Registers-In-Python.html#Registers-In-Python)），用于`reggroup`中的所有寄存器。


Function: **Architecture.register_groups** *()*

> 功能：**Architecture.register_groups** *（）*


:   Return a `gdb.RegisterGroupsIterator` (see [Registers In Python](Registers-In-Python.html#Registers-In-Python)) for all of the register groups available for the `gdb.Architecture`.

> 返回一个`gdb.RegisterGroupsIterator`（参见[Python中的寄存器](Registers-In-Python.html#Registers-In-Python)），用于`gdb.Architecture`可用的所有寄存器组。

---

::: header
Next: [Registers In Python](Registers-In-Python.html#Registers-In-Python)]
:::
