---
tip: translate by openai@2023-06-23 21:27:17
...
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

> 调用堆栈被划分成连续的部分，称为堆栈帧，或简称帧；每个帧是与一次函数调用相关联的数据。该帧包含给定给函数的参数、函数的局部变量以及函数正在执行的地址。


When your program is started, the stack has only one frame, that of the function `main`. This is called the *initial* frame or the *outermost* frame. Each time a function is called, a new frame is made. Each time a function returns, the frame for that function invocation is eliminated. If a function is recursive, there can be many frames for the same function. The frame for the function in which execution is actually occurring is called the *innermost* frame. This is the most recently created of all the stack frames that still exist.

> 当你的程序开始时，堆栈只有一个帧，即函数'main'的帧。这被称为*初始*帧或*最外层*帧。每次调用函数时，都会创建一个新帧。每次函数返回时，该函数调用的帧都会被消除。如果函数是递归的，同一个函数可能有多个帧。正在执行的函数的帧称为*最内层*帧。这是所有仍然存在的堆栈帧中最新创建的帧。


Inside your program, stack frames are identified by their addresses. A stack frame consists of many bytes, each of which has its own address; each kind of computer has a convention for choosing one byte whose address serves as the address of the frame. Usually this address is kept in a register called the *frame pointer register* (see [\$fp](Registers.html#Registers)) while execution is going on in that frame.

> 在你的程序中，堆栈帧是通过它们的地址来识别的。堆栈帧由许多字节组成，每个字节都有自己的地址；每种计算机都有一种约定，用于选择一个字节，其地址用作帧的地址。通常，在该帧中执行时，该地址会存储在一个叫做*帧指针寄存器*的寄存器中（参见[\$fp](Registers.html#Registers))。


[GDB] commands. The terms *frame number* and *frame level* can be used interchangeably to describe this number.

> [GDB] 命令。术语*帧号*和*帧级*可以互换使用来描述这个数字。


Some compilers provide a way to compile functions so that they operate without stack frames. (For example, the [GCC] option

> 一些编译器提供一种方法来编译函数，使它们在没有堆栈帧的情况下运行。（例如，[GCC]选项

::: smallexample

```bash
‘-fomit-frame-pointer’
```

:::


generates functions without a frame.) This is occasionally done with heavily used library functions to save the frame setup time. [GDB] has no provision for frameless functions elsewhere in the stack.

> 生成无框架的函数。这通常会用于频繁使用的库函数，以节省框架设置时间。[GDB]在堆栈的其他位置没有提供无框架函数的规定。

---

::: header
Next: [Backtrace](Backtrace.html#Backtrace)]
:::
