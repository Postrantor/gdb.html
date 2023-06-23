---
description: Frames (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Frames (Debugging with GDB)
lang: en
resource-type: document
title: Frames (Debugging with GDB)
---
::: header
Next: [Backtrace](Backtrace.html#Backtrace)]
:::

---

### 8.1 Stack Frames

The call stack is divided up into contiguous pieces called *stack frames*, or *frames* for short; each frame is the data associated with one call to one function. The frame contains the arguments given to the function, the function's local variables, and the address at which the function is executing.

When your program is started, the stack has only one frame, that of the function `main`. This is called the *initial* frame or the *outermost* frame. Each time a function is called, a new frame is made. Each time a function returns, the frame for that function invocation is eliminated. If a function is recursive, there can be many frames for the same function. The frame for the function in which execution is actually occurring is called the *innermost* frame. This is the most recently created of all the stack frames that still exist.

Inside your program, stack frames are identified by their addresses. A stack frame consists of many bytes, each of which has its own address; each kind of computer has a convention for choosing one byte whose address serves as the address of the frame. Usually this address is kept in a register called the *frame pointer register* (see [\$fp](Registers.html#Registers)) while execution is going on in that frame.

[GDB] commands. The terms *frame number* and *frame level* can be used interchangeably to describe this number.

Some compilers provide a way to compile functions so that they operate without stack frames. (For example, the [GCC] option

::: smallexample

```bash
‘-fomit-frame-pointer’
```

:::

generates functions without a frame.) This is occasionally done with heavily used library functions to save the frame setup time. [GDB] has no provision for frameless functions elsewhere in the stack.

---

::: header
Next: [Backtrace](Backtrace.html#Backtrace)]
:::
