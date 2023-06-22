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

- Tracepoint expressions are intended to gather objects (lvalues). Thus the full flexibility of GDB's expression evaluator is not available. You cannot call functions, cast objects to aggregate types, access convenience variables or modify values (except by assignment to trace state variables). Some language features may implicitly call functions (for instance Objective-C fields with accessors), and therefore cannot be collected either.
- Collection of local variables, either individually or in bulk with `$locals` or `$args`, during `while-stepping` may behave erratically. The stepping action may enter a new scope (for instance by stepping into a function), or the location of the variable may change (for instance it is loaded into a register). The tracepoint data recorded uses the location information for the variables that is correct for the tracepoint location. When the tracepoint is created, it is not possible, in general, to determine where the steps of a `while-stepping` sequence will advance the program---particularly if a conditional branch is stepped.
- Collection of an incompletely-initialized or partially-destroyed object may result in something that [GDB] cannot display, or displays in a misleading way.
- When [GDB] displays a pointer to character it automatically dereferences the pointer to also display characters of the string being pointed to. However, collecting the pointer during tracing does not automatically collect the string. You need to explicitly dereference the pointer and provide size information if you want to collect not only the pointer, but the memory pointed to. For example, `*ptr@50` can be used to collect the 50 element array pointed to by `ptr`.
- It is not possible to collect a complete stack backtrace at a tracepoint. Instead, you may collect the registers and a few hundred bytes from the stack pointer with something like `*(unsigned char *)$esp@300` (adjust to use the name of the actual stack pointer register on your target architecture, and the amount of stack you wish to capture). Then the `backtrace` command will show a partial backtrace when using a trace frame. The number of stack frames that can be examined depends on the sizes of the frames in the collected stack. Note that if you ask for a block so large that it goes past the bottom of the stack, the target agent may report an error trying to read from an invalid address.
- If you do not collect registers at a tracepoint, [GDB] will warn you that it can't infer `$pc`, and default it to zero.

---

::: header
Previous: [Starting and Stopping Trace Experiments](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments)]
:::
