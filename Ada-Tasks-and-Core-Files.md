---
description: Ada Tasks and Core Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Tasks and Core Files (Debugging with GDB)
lang: en
resource-type: document
title: Ada Tasks and Core Files (Debugging with GDB)
---
::: header
Next: [Ravenscar Profile](Ravenscar-Profile.html#Ravenscar-Profile)]
:::

---

#### 15.4.10.8 Tasking Support when Debugging Core Files

When inspecting a core file, as opposed to debugging a live program, tasking support may be limited or even unavailable, depending on the platform being used. For instance, on x86-linux, the list of tasks is available, but task switching is not supported.

On certain platforms, the debugger needs to perform some memory writes in order to provide Ada tasking support. When inspecting a core file, this means that the core file must be opened with read-write privileges, using the command '`"set write on"`.
