---
tip: translate by openai@2023-06-23 23:30:19
...
---
description: Inline Functions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Inline Functions (Debugging with GDB)
lang: en
resource-type: document
title: Inline Functions (Debugging with GDB)
---
::: header
Next: [Tail Call Frames](Tail-Call-Frames.html#Tail-Call-Frames)]
:::

---

### 11.1 Inline Functions


*Inlining* is an optimization that inserts a copy of the function body directly at each call site, instead of jumping to a shared routine. [GDB] displays inlined functions just like non-inlined functions. They appear in backtraces. You can view their arguments and local variables, step into them with `step`, skip them with `next`, and escape from them with `finish`. You can check whether a function was inlined by using the `info frame` command.

> *内联*是一种优化，它将函数体的副本直接插入到每个调用站点，而不是跳转到共享例程。 [GDB] 显示的内联函数就像非内联函数一样。它们出现在回溯中。您可以查看它们的参数和局部变量，使用`step`进入它们，使用`next`跳过它们，并使用`finish`从它们中逃脱。您可以通过使用`info frame`命令检查函数是否被内联。


For [GDB]. It instead displays the arguments and local variables of inlined functions as local variables in the caller.

> 对于[GDB]，它会将内联函数的参数和局部变量显示为调用者的局部变量。


The body of an inlined function is directly included at its call site; unlike a non-inlined function, there are no instructions devoted to the call. [GDB] still pretends that the call site and the start of the inlined function are different instructions. Stepping to the call site shows the call site, and then stepping again shows the first line of the inlined function, even though no additional instructions are executed.

> 被内联的函数的正文直接包含在其调用站点中；与非内联函数不同，没有指令专门用于调用。 [GDB] 仍然假装调用站点和内联函数的开头是不同的指令。跳转到调用站点显示调用站点，然后再跳一次显示内联函数的第一行，即使没有执行额外的指令。


This makes source-level debugging much clearer; you can see both the context of the call and then the effect of the call. Only stepping by a single instruction using `stepi` or `nexti` does not do this; single instruction steps always show the inlined body.

> 这使源级调试变得更加清晰；您可以看到调用的上下文以及调用的效果。仅使用`stepi`或`nexti`逐条执行不能做到这一点；单条指令的步进总是显示内联体。


There are some ways that [GDB] does not pretend that inlined function calls are the same as normal calls:

> GDB不假装内联函数调用和正常调用是一样的，有一些方法可以证明这一点。


- Setting breakpoints at the call site of an inlined function may not work, because the call site does not contain any code. [GDB]; until then, set a breakpoint on an earlier line or inside the inlined function instead.

> 设置在内联函数调用处的断点可能不起作用，因为调用处不包含任何代码。[GDB]；在此之前，请在更早的行或内联函数内设置断点。
- [GDB] cannot locate the return value of inlined calls after using the `finish` command. This is a limitation of compiler-generated debugging information; after `finish`, you can step to the next line and print a variable where your program stored the return value.

---

::: header
Next: [Tail Call Frames](Tail-Call-Frames.html#Tail-Call-Frames)]
:::
