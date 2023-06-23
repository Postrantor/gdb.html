---
tip: translate by openai@2023-06-23 16:23:29
...
---
description: Tracepoint Restrictions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Tracepoint Restrictions (Debugging with GDB)
lang: en
resource-type: document
title: Tracepoint Restrictions (Debugging with GDB)
---------------------------------------------------

::: header
Previous: [Starting and Stopping Trace Experiments](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments)]
:::

---

#### 13.1.10 Tracepoint Restrictions

There are a number of restrictions on the use of tracepoints. As described above, tracepoint data gathering occurs on the target without interaction from [GDB]. Thus the full capabilities of the debugger are not available during data gathering, and then at data examination time, you will be limited by only having what was collected. The following items describe some common problems, but it is not exhaustive, and you may run into additional difficulties not mentioned here.

> 有许多限制使用跟踪点。正如上面所述，跟踪点数据收集发生在目标上，而不需要[GDB]的交互。因此，在数据收集期间不可用调试器的全部功能，而在数据检查时，您将受限于只有所收集的内容。以下项目描述了一些常见问题，但这不是详尽的，您可能会遇到未在此处提及的其他困难。

- Tracepoint expressions are intended to gather objects (lvalues). Thus the full flexibility of GDB's expression evaluator is not available. You cannot call functions, cast objects to aggregate types, access convenience variables or modify values (except by assignment to trace state variables). Some language features may implicitly call functions (for instance Objective-C fields with accessors), and therefore cannot be collected either.

> 跟踪点表达式旨在收集对象（lvalues）。因此 GDB 表达式求值器的全部灵活性不可用。您不能调用函数，将对象转换为聚合类型，访问便利变量或修改值（除了对跟踪状态变量的赋值）。某些语言特性可能会隐式调用函数（例如具有访问器的 Objective-C 字段），因此也无法收集。

- Collection of local variables, either individually or in bulk with `$locals` or `$args`, during `while-stepping` may behave erratically. The stepping action may enter a new scope (for instance by stepping into a function), or the location of the variable may change (for instance it is loaded into a register). The tracepoint data recorded uses the location information for the variables that is correct for the tracepoint location. When the tracepoint is created, it is not possible, in general, to determine where the steps of a `while-stepping` sequence will advance the program---particularly if a conditional branch is stepped.

> 收集局部变量（单独或使用$locals或$args）在 while-stepping 期间可能会表现出不稳定的行为。探测动作可能会进入新的作用域（例如通过跳入函数），或者变量的位置可能会改变（例如它被加载到寄存器中）。记录的跟踪点数据使用的是跟踪点位置的变量位置信息。当跟踪点被创建时，通常无法确定 while-stepping 序列的步骤将如何推进程序，特别是如果跳入条件分支时。

- Collection of an incompletely-initialized or partially-destroyed object may result in something that [GDB] cannot display, or displays in a misleading way.

> 收集不完全初始化或部分销毁的对象可能会导致[GDB]无法显示或以误导的方式显示。

- When [GDB] displays a pointer to character it automatically dereferences the pointer to also display characters of the string being pointed to. However, collecting the pointer during tracing does not automatically collect the string. You need to explicitly dereference the pointer and provide size information if you want to collect not only the pointer, but the memory pointed to. For example, `*ptr@50` can be used to collect the 50 element array pointed to by `ptr`.

> 当 GDB 显示指向字符的指针时，它会自动解引用指针，以显示指向的字符串的字符。但是，在跟踪过程中收集指针时不会自动收集字符串。如果您想要收集指针，并且还要收集指向的内存，则需要显式解引用指针并提供大小信息。例如，可以使用 `*ptr@50` 来收集由 `ptr` 指向的 50 个元素数组。

- It is not possible to collect a complete stack backtrace at a tracepoint. Instead, you may collect the registers and a few hundred bytes from the stack pointer with something like `*(unsigned char *)$esp@300` (adjust to use the name of the actual stack pointer register on your target architecture, and the amount of stack you wish to capture). Then the `backtrace` command will show a partial backtrace when using a trace frame. The number of stack frames that can be examined depends on the sizes of the frames in the collected stack. Note that if you ask for a block so large that it goes past the bottom of the stack, the target agent may report an error trying to read from an invalid address.

> 不可能在跟踪点收集完整的堆栈跟踪。相反，您可以使用类似 `*（unsigned char *）$esp @ 300`（根据目标体系结构调整以使用实际堆栈指针寄存器的名称，以及您想捕获的堆栈大小）收集寄存器和从堆栈指针开始的几百个字节。然后，使用跟踪帧时，`backtrace` 命令将显示部分跟踪。可以检查的堆栈帧数量取决于收集堆栈中帧的大小。请注意，如果您请求的块太大，以至于超出堆栈底部，则目标代理可能会报告尝试从无效地址读取时出错的错误。

- If you do not collect registers at a tracepoint, [GDB] will warn you that it can't infer `$pc`, and default it to zero.

> 如果你没有在跟踪点收集寄存器，[GDB]会警告你无法推断 `$pc`，并将其默认为零。

---

::: header
Previous: [Starting and Stopping Trace Experiments](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments)]
:::
