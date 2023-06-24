---
tip: translate by openai@2023-06-23 20:17:16
...
---
description: Debug Session (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Debug Session (Debugging with GDB)
lang: en
resource-type: document
title: Debug Session (Debugging with GDB)
---
::: header
Previous: [Bootstrapping](Bootstrapping.html#Bootstrapping)]
:::

---

#### 20.5.3 Putting it All Together


In summary, when your program is ready to debug, you must follow these steps.

> 总之，当你的程序准备调试时，你必须按照以下步骤进行。


1. Make sure you have defined the supporting low-level routines (see [What You Must Do for the Stub](Bootstrapping.html#Bootstrapping)):

> 确保你已经定义了支持的低级例程（参见[你必须为存根做什么]（Bootstrapping.html＃Bootstrapping））：

   ::: display

   ```display
   getDebugChar, putDebugChar,
   flush_i_cache, memset, exceptionHandler.
   ```

   :::

2. Insert these lines in your program's startup code, before the main procedure is called:

> 在主程序被调用之前，将这些行插入到程序的启动代码中：

   ::: smallexample

   ```bash
   set_debug_traps();
   breakpoint();
   ```

   :::


   On some machines, when a breakpoint trap is raised, the hardware automatically makes the PC point to the instruction after the breakpoint. If your machine doesn't do that, you may need to adjust `handle_exception` to arrange for it to return to the instruction after the breakpoint on this first invocation, so that your program doesn't keep hitting the initial breakpoint instead of making progress.

> 在某些机器上，当触发断点陷阱时，硬件会自动使PC指向断点后的指令。如果您的机器不能做到这一点，您可能需要调整“handle_exception”，以便在第一次调用时将其指向断点后的指令，以便您的程序不会一直撞击最初的断点，而是继续前进。

3. For the 680x0 stub only, you need to provide a variable called `exceptionHook`. Normally you just use:

> 对于680x0存根，您需要提供一个叫做“exceptionHook”的变量。通常只需使用：

   ::: smallexample

   ```bash
   void (*exceptionHook)() = 0;
   ```

   :::


   but if before calling `set_debug_traps`, you set it to point to a function in your program, that function is called when `GDB` continues after stopping on a trap (for example, bus error). The function indicated by `exceptionHook` is called with one parameter: an `int` which is the exception number.

> 如果在调用“set_debug_traps”之前，将其指向程序中的一个函数，则在GDB在遇到陷阱（例如总线错误）后继续时，将调用该函数。 由exceptionHook指示的函数带有一个参数：int，它是异常号。

4. Compile and link together: your program, the [GDB] debugging stub for your target architecture, and the supporting subroutines.

> 编译并链接：你的程序、你目标架构的[GDB]调试桩和支持的子程序。

5. Make sure you have a serial connection between your target machine and the [GDB] host, and identify the serial port on the host.

> 确保你的目标机器和[GDB]主机之间有串行连接，并确定主机上的串行端口。

6. Download your program to your target machine (or get it there by whatever means the manufacturer provides), and start it.

> 下载程序到目标机器（或者按照制造商提供的任何方式获取），然后启动它。

7. Start [GDB] on the host, and connect to the target (see [Connecting to a Remote Target](Connecting.html#Connecting)).

> 开始在主机上启动GDB，并连接到目标（参见[连接到远程目标](Connecting.html#Connecting)）。

---

::: header
Previous: [Bootstrapping](Bootstrapping.html#Bootstrapping)]
:::
