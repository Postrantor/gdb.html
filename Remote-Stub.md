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

To debug a program running on another machine (the debugging *target* machine), you must first arrange for all the usual prerequisites for the program to run by itself. For example, for a C program, you need:

1. A startup routine to set up the C runtime environment; these usually have a name like `crt0`. The startup routine may be supplied by your hardware supplier, or you may have to write your own.
2. A C subroutine library to support your program's subroutine calls, notably managing input and output.
3. A way of getting your program to the other machine---for example, a download program. These are often supplied by the hardware manufacturer, but you may have to write your own from hardware documentation.

The next step is to arrange for your program to use a serial port to communicate with the machine where [GDB] is running (the *host* machine). In general terms, the scheme looks like this:

*On the host,*

:   [GDB]' command (see [Specifying a Debugging Target](Targets.html#Targets)).

*On the target,*

:   you must link with your program a few special-purpose subroutines that implement the [GDB] remote serial protocol. The file containing these subroutines is called a *debugging stub*.

```
On certain remote targets, you can use an auxiliary program `gdbserver` instead of linking a stub into your program. See [Using the `gdbserver` Program](Server.html#Server), for details.
```

The debugging stub is specific to the architecture of the remote machine; for example, use `sparc-stub.c` boards.

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
• [Bootstrapping](Bootstrapping.html#Bootstrapping):        What you must do for the stub
• [Debug Session](Debug-Session.html#Debug-Session):        Putting it all together

---

---

::: header
Previous: [Remote Configuration](Remote-Configuration.html#Remote-Configuration)]
:::
