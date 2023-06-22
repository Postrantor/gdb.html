---
description: Debugger Adapter Protocol (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Debugger Adapter Protocol (Debugging with GDB)
lang: en
resource-type: document
title: Debugger Adapter Protocol (Debugging with GDB)
---
::: header
Next: [JIT Interface](JIT-Interface.html#JIT-Interface)]
:::

---

## 29 Debugger Adapter Protocol

Generally, [GDB] implements the Debugger Adapter Protocol as written. However, in some cases, extensions are either needed or even expected.

[GDB] defines some parameters that can be passed to the `launch` request:

`args`

:   If provided, this should be an array of strings. These strings are provided as command-line arguments to the inferior, as if by `set args`. See [Arguments](Arguments.html#Arguments).

`env`

:   If provided, this should be an object. Each key of the object will be used as the name of an environment variable; each value must be a string and will be the value of that variable. The environment of the inferior will be set to exactly as passed in. See [Environment](Environment.html#Environment).

`program`

:   If provided, this is a string that specifies the program to use. This corresponds to the `file` command. See [Files](Files.html#Files).

`stopAtBeginningOfMainSubprogram`

:   If provided, this must be a boolean. When '`True` will set a temporary breakpoint at the program's main procedure, using the same approach as the `start` command. See [Starting](Starting.html#Starting).

[GDB] defines some parameters that can be passed to the `attach` request. One of these must be specified.

`pid`

:   The process ID to which [GDB] should attach. See [Attach](Attach.html#Attach).

`target`

:   The target to which [GDB] should connect. This is a string and is passed to the `target remote` command. See [Connecting](Connecting.html#Connecting).
