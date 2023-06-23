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

It is possible to build [GDB] command.

`set architecture arch`

This command sets the current target architecture to `arch` can be `"auto"`, in addition to one of the supported architectures.

`show architecture`

Show the current target architecture.

`set processor`

`processor`

These are alias commands for, respectively, `set architecture` and `show architecture`.

---

• [Active Targets](Active-Targets.html#Active-Targets):           Active targets
• [Target Commands](Target-Commands.html#Target-Commands):        Commands for managing targets
• [Byte Order](Byte-Order.html#Byte-Order):                       Choosing target byte order

---
