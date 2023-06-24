---
tip: translate by openai@2023-06-24 04:11:50
...
---
description: Tracepoint Restrictions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Tracepoint Restrictions (Debugging with GDB)
lang: en
resource-type: document
title: Tracepoint Restrictions (Debugging with GDB)
---
::: header
Previous: [Starting and Stopping Trace Experiments](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments)]
:::

---

#### 13.1.10 Tracepoint Restrictions


There are a number of restrictions on the use of tracepoints. As described above, tracepoint data gathering occurs on the target without interaction from [GDB]. Thus the full capabilities of the debugger are not available during data gathering, and then at data examination time, you will be limited by only having what was collected. The following items describe some common problems, but it is not exhaustive, and you may run into additional difficulties not mentioned here.

> 有许多限制使用跟踪点。正如上述所述，跟踪点数据收集发生在目标上，而无需[GDB]的交互。因此，在数据收集期间，调试器的全部功能不可用，然后在数据检查时，您将受限于只有收集的内容。以下项目描述了一些常见问题，但这不是详尽的，您可能会遇到未在此处提及的其他困难。


- Tracepoint expressions are intended to gather objects (lvalues). Thus the full flexibility of GDB's expression evaluator is not available. You cannot call functions, cast objects to aggregate types, access convenience variables or modify values (except by assignment to trace state variables). Some language features may implicitly call functions (for instance Objective-C fields with accessors), and therefore cannot be collected either.

> 跟踪点表达式旨在收集对象（lvalues）。因此，GDB表达式评估器的全部灵活性不可用。您不能调用函数，将对象转换为聚合类型，访问便利变量或修改值（除非分配给跟踪状态变量）。某些语言特性可能会隐式调用函数（例如带有访问器的Objective-C字段），因此也无法收集。

- Collection of local variables, either individually or in bulk with `$locals` or `$args`, during `while-stepping` may behave erratically. The stepping action may enter a new scope (for instance by stepping into a function), or the location of the variable may change (for instance it is loaded into a register). The tracepoint data recorded uses the location information for the variables that is correct for the tracepoint location. When the tracepoint is created, it is not possible, in general, to determine where the steps of a `while-stepping` sequence will advance the program---particularly if a conditional branch is stepped.

> 在`while-stepping`期间，本地变量的集合，单独或通过`$locals`或`$args`批量收集，可能表现不稳定。步进操作可能进入一个新的作用域（例如通过步入一个函数），或者变量的位置可能会改变（例如它被加载到一个寄存器中）。记录的跟踪点数据使用的是与跟踪点位置相关的变量位置信息。当跟踪点被创建时，通常无法确定`while-stepping`序列的步骤将会将程序推进到何处，尤其是如果是条件分支被步进的情况。

- Collection of an incompletely-initialized or partially-destroyed object may result in something that [GDB] cannot display, or displays in a misleading way.

> 收集不完全初始化或部分销毁的对象可能会导致[GDB]无法显示或以误导性方式显示。

- When [GDB] displays a pointer to character it automatically dereferences the pointer to also display characters of the string being pointed to. However, collecting the pointer during tracing does not automatically collect the string. You need to explicitly dereference the pointer and provide size information if you want to collect not only the pointer, but the memory pointed to. For example, `*ptr@50` can be used to collect the 50 element array pointed to by `ptr`.

> 当GDB显示指向字符的指针时，它会自动解引用指针，以显示指向的字符串。但是，在跟踪时收集指针不会自动收集字符串。您需要显式解引用指针，并提供大小信息，如果您想收集指针以及指向的内存，可以使用`*ptr@50`来收集由`ptr`指向的50个元素数组。

- It is not possible to collect a complete stack backtrace at a tracepoint. Instead, you may collect the registers and a few hundred bytes from the stack pointer with something like `*(unsigned char *)$esp@300` (adjust to use the name of the actual stack pointer register on your target architecture, and the amount of stack you wish to capture). Then the `backtrace` command will show a partial backtrace when using a trace frame. The number of stack frames that can be examined depends on the sizes of the frames in the collected stack. Note that if you ask for a block so large that it goes past the bottom of the stack, the target agent may report an error trying to read from an invalid address.

> 不可能在跟踪点收集完整的堆栈跟踪。相反，您可以使用类似`*（unsigned char *）$ esp @ 300`的指令收集寄存器和从堆栈指针收集的几百个字节（根据您的目标架构调整使用堆栈指针寄存器的名称以及要收集的堆栈大小）。然后，使用跟踪框架时，`backtrace`命令将显示部分跟踪。可以检查的堆栈帧数量取决于收集的堆栈中的帧大小。请注意，如果要求的块太大，以至于它超出了堆栈底部，则目标代理可能会报告尝试从无效地址读取时出错。

- If you do not collect registers at a tracepoint, [GDB] will warn you that it can't infer `$pc`, and default it to zero.

> 如果您没有在跟踪点收集寄存器，[GDB]会警告您无法推断出“$pc”，并将其默认为零。

---

::: header
Previous: [Starting and Stopping Trace Experiments](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments)]
:::
