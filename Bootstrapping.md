---
tip: translate by openai@2023-06-23 18:07:02
...
---
description: Bootstrapping (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Bootstrapping (Debugging with GDB)
lang: en
resource-type: document
title: Bootstrapping (Debugging with GDB)
---
::: header
Next: [Debug Session](Debug-Session.html#Debug-Session)]
:::

---

#### 20.5.2 What You Must Do for the Stub


The debugging stubs that come with [GDB] are set up for a particular chip architecture, but they have no information about the rest of your debugging target machine.

> 调试存根，随[GDB]一起提供，是为特定芯片架构设置的，但它们没有有关您的调试目标机器的其他信息。


First of all you need to tell the stub how to communicate with the serial port.

> 首先，您需要告诉存根如何与串行端口进行通信。

`int getDebugChar()`


Write this subroutine to read a single character from the serial port. It may be identical to `getchar` for your target system; a different name is used to allow you to distinguish the two if you wish.

> 编写这个子程序从串口读取单个字符。 对于您的目标系统，它可能与`getchar`相同； 使用不同的名称可以让您区分两者。

`void putDebugChar(int)`


Write this subroutine to write a single character to the serial port. It may be identical to `putchar` for your target system; a different name is used to allow you to distinguish the two if you wish.

> 请编写这个子程序，将一个字符写入串口。 对于您的目标系统，它可能与`putchar`相同; 为了使您能够区分这两者，使用了不同的名称。


If you want [GDB] uses to tell the remote system to stop.

> 如果你想要GDB使用来告诉远程系统停止，


Getting the debugging target to return the proper status to [GDB] reports a `SIGTRAP` instead of a `SIGINT`).

> 让调试目标返回正确的状态给GDB，而不是返回SIGINT，而是返回SIGTRAP。


Other routines you need to supply are:

> 你需要提供的其他例行程序是：

`void exceptionHandler (int exception_number, void *exception_address)`


Write this function to install `exception_address`, it should be a simple jump, not a jump to subroutine.

> 写一个函数来安装exception_address，应该是一个简单的跳转，而不是跳转到子程序。


For the 386, `exception_address` and 68k stubs are able to mask interrupts themselves without help from `exceptionHandler`.

> 对于386，exception_address和68k存根可以在没有exceptionHandler帮助的情况下自行掩盖中断。

`void flush_i_cache()`


On [SPARC] only, write this subroutine to flush the instruction cache, if any, on your target machine. If there is no instruction cache, this subroutine may be a no-op.

> 在[SPARC]上，编写此子程序以清空目标机器上的指令高速缓存（如果有的话）。如果没有指令高速缓存，此子程序可能是空操作。


On target machines that have instruction caches, [GDB] requires this function to make certain that the state of your program is stable.

> 在具有指令缓存的目标机上，[GDB]需要这个函数来确保你的程序的状态是稳定的。


You must also make sure this library routine is available:

> 你也必须确保这个库例程可用：

`void *memset(void *, int, int)`


This is the standard library function `memset` that sets an area of memory to a known value. If you have one of the free versions of `libc.a`, `memset` can be found there; otherwise, you must either obtain it from your hardware manufacturer, or write your own.

> 这是标准库函数`memset`，它将内存的一块区域设置为已知的值。如果你有免费版本的`libc.a`，你可以在那里找到`memset`；否则，你必须从你的硬件制造商那里获得它，或者自己编写。


If you do not use the GNU C compiler, you may need other standard library subroutines as well; this varies from one stub to another, but in general the stubs are likely to use any of the common library subroutines which `GCC` generates as inline code.

> 如果您不使用GNU C 编译器，您可能还需要其他标准库子程序；这取决于一个存根和另一个存根，但一般来说，存根可能会使用GCC生成的任何常用库子程序作为内联代码。

---

::: header
Next: [Debug Session](Debug-Session.html#Debug-Session)]
:::
