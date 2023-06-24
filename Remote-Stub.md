---
tip: translate by openai@2023-06-24 02:07:54
...
---
description: Remote Stub (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Remote Stub (Debugging with GDB)
lang: en
resource-type: document
title: Remote Stub (Debugging with GDB)
---
::: header
Previous: [Remote Configuration](Remote-Configuration.html#Remote-Configuration)]
:::

---

### 20.5 Implementing a Remote Stub


The stub files provided with [GDB] is the best organized, and therefore the easiest to read.)

> 提供的[GDB]存根文件是最好组织的，因此最容易阅读。


To debug a program running on another machine (the debugging *target* machine), you must first arrange for all the usual prerequisites for the program to run by itself. For example, for a C program, you need:

> 要在另一台机器（调试目标机）上调试程序，首先必须安排程序本身运行所需的所有常规先决条件。例如，对于C程序，您需要：


1. A startup routine to set up the C runtime environment; these usually have a name like `crt0`. The startup routine may be supplied by your hardware supplier, or you may have to write your own.

> 1. 一个启动例程，用于设置C运行时环境；通常有一个名字，如crt0。启动例程可能由您的硬件供应商提供，或者您可能需要自己编写。

2. A C subroutine library to support your program's subroutine calls, notably managing input and output.

> 2. 一个C子程序库，用于支持程序的子程序调用，特别是管理输入和输出。

3. A way of getting your program to the other machine---for example, a download program. These are often supplied by the hardware manufacturer, but you may have to write your own from hardware documentation.

> 3. 一种将程序传输到其他机器的方式---例如，下载程序。通常由硬件制造商提供，但您可能需要从硬件文档中编写自己的程序。


The next step is to arrange for your program to use a serial port to communicate with the machine where [GDB] is running (the *host* machine). In general terms, the scheme looks like this:

> 下一步是安排你的程序使用串行端口与运行[GDB]的机器（主机机器）通信。一般来说，该方案如下：

*On the host,*


:   [GDB]' command (see [Specifying a Debugging Target](Targets.html#Targets)).

> [GDB] 命令（参见[指定调试目标](Targets.html#Targets)）。

*On the target,*


:   you must link with your program a few special-purpose subroutines that implement the [GDB] remote serial protocol. The file containing these subroutines is called a *debugging stub*.

> 你必须将一些特殊用途的子程序与你的程序链接起来，以实现[GDB]远程串行协议。包含这些子程序的文件称为调试存根。

```
On certain remote targets, you can use an auxiliary program `gdbserver` instead of linking a stub into your program. See [Using the `gdbserver` Program](Server.html#Server), for details.
```


The debugging stub is specific to the architecture of the remote machine; for example, use `sparc-stub.c` boards.

> 调试存根是专门针对远程机器的架构的；例如，使用`sparc-stub.c`板。

These working remote stubs are distributed with [GDB]:

`i386-stub.c`

:

```
For Intel 386 and compatible architectures.
```

`m68k-stub.c`

:

```
For Motorola 680x0 architectures.
```

`sh-stub.c`

:

```
For Renesas SH architectures.
```

`sparc-stub.c`

:

```
For [SPARC] architectures.
```

`sparcl-stub.c`

:

```
For Fujitsu [SPARCLITE] architectures.
```

The `README` distribution may list other recently added stubs.

---


• [Stub Contents](Stub-Contents.html#Stub-Contents):        What the stub can do for you

> • [存根内容](Stub-Contents.html#Stub-Contents): 存根能为您做什么？

• [Bootstrapping](Bootstrapping.html#Bootstrapping):        What you must do for the stub

> • [引导](Bootstrapping.html#Bootstrapping)：你必须为存根做什么？

• [Debug Session](Debug-Session.html#Debug-Session):        Putting it all together

> • [调试会话](Debug-Session.html#Debug-Session):        把它们全部放在一起

---

---

::: header
Previous: [Remote Configuration](Remote-Configuration.html#Remote-Configuration)]
:::
