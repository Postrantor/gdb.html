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

A `gdb.Architecture` class has the following methods:

Function: **Architecture.name** *()*

:   Return the name (string value) of the architecture.

```
<!-- -->
```

)*

:   Return a list of disassembled instructions starting from the memory address `start_pc` is returned. For all of these cases, each element of the returned list is a Python `dict` with the following string keys:

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

```
`size` is the size, in bits, of the desired integer type. Only certain sizes are currently supported: 0, 8, 16, 24, 32, 64, and 128.

If `signed` is `False`, the returned type will be unsigned.

If the indicated type cannot be found, this function will throw a `ValueError` exception.
```

)*

:   Return a `gdb.RegisterDescriptorIterator` (see [Registers In Python](Registers-In-Python.html#Registers-In-Python)) for all of the registers in `reggroup`' is assumed.

Function: **Architecture.register_groups** *()*

:   Return a `gdb.RegisterGroupsIterator` (see [Registers In Python](Registers-In-Python.html#Registers-In-Python)) for all of the register groups available for the `gdb.Architecture`.

---

::: header
Next: [Registers In Python](Registers-In-Python.html#Registers-In-Python)]
:::
