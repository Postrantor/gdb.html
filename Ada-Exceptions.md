---
description: Ada Exceptions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Exceptions (Debugging with GDB)
lang: en
resource-type: document
title: Ada Exceptions (Debugging with GDB)
---
::: header
Next: [Ada Tasks](Ada-Tasks.html#Ada-Tasks)]
:::

---

#### 15.4.10.6 Ada Exceptions

A command is provided to list all Ada exceptions:

`info exceptions`

`info exceptions regexp`

The `info exceptions` command allows you to list all Ada exceptions defined within the program being debugged, as well as their addresses. With a regular expression, `regexp` are listed.

Below is a small example, showing how the command can be used, first without argument, and next with a regular expression passed as an argument.

::: smallexample

```bash
(gdb) info exceptions
All defined Ada exceptions:
constraint_error: 0x613da0
program_error: 0x613d20
storage_error: 0x613ce0
tasking_error: 0x613ca0
const.aint_global_e: 0x613b00
(gdb) info exceptions const.aint
All Ada exceptions matching regular expression "const.aint":
constraint_error: 0x613da0
const.aint_global_e: 0x613b00
```

:::

It is also possible to ask [GDB] to stop your program's execution when an exception is raised. For more details, see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints).
