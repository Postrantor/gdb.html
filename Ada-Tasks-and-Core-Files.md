---
tip: translate by openai@2023-06-23 16:59:32
...
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

> 在检查核心文件时，与调试实时程序相比，任务支持可能受到限制，甚至不可用，这取决于使用的平台。例如，在x86-linux上，任务列表是可用的，但不支持任务切换。


On certain platforms, the debugger needs to perform some memory writes in order to provide Ada tasking support. When inspecting a core file, this means that the core file must be opened with read-write privileges, using the command '`"set write on"`.

> 在某些平台上，调试器需要执行一些内存写入操作，以提供Ada任务支持。当检查核心文件时，这意味着必须使用命令“set write on”以读写权限打开核心文件。
