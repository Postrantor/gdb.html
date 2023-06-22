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

For [GDB]. It instead displays the arguments and local variables of inlined functions as local variables in the caller.

The body of an inlined function is directly included at its call site; unlike a non-inlined function, there are no instructions devoted to the call. [GDB] still pretends that the call site and the start of the inlined function are different instructions. Stepping to the call site shows the call site, and then stepping again shows the first line of the inlined function, even though no additional instructions are executed.

This makes source-level debugging much clearer; you can see both the context of the call and then the effect of the call. Only stepping by a single instruction using `stepi` or `nexti` does not do this; single instruction steps always show the inlined body.

There are some ways that [GDB] does not pretend that inlined function calls are the same as normal calls:

- Setting breakpoints at the call site of an inlined function may not work, because the call site does not contain any code. [GDB]; until then, set a breakpoint on an earlier line or inside the inlined function instead.
- [GDB] cannot locate the return value of inlined calls after using the `finish` command. This is a limitation of compiler-generated debugging information; after `finish`, you can step to the next line and print a variable where your program stored the return value.

---

::: header
Next: [Tail Call Frames](Tail-Call-Frames.html#Tail-Call-Frames)]
:::
