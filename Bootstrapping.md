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

First of all you need to tell the stub how to communicate with the serial port.

`int getDebugChar()`

Write this subroutine to read a single character from the serial port. It may be identical to `getchar` for your target system; a different name is used to allow you to distinguish the two if you wish.

`void putDebugChar(int)`

Write this subroutine to write a single character to the serial port. It may be identical to `putchar` for your target system; a different name is used to allow you to distinguish the two if you wish.

If you want [GDB] uses to tell the remote system to stop.

Getting the debugging target to return the proper status to [GDB] reports a `SIGTRAP` instead of a `SIGINT`).

Other routines you need to supply are:

`void exceptionHandler (int exception_number, void *exception_address)`

Write this function to install `exception_address`, it should be a simple jump, not a jump to subroutine.

For the 386, `exception_address` and 68k stubs are able to mask interrupts themselves without help from `exceptionHandler`.

`void flush_i_cache()`

On [SPARC] only, write this subroutine to flush the instruction cache, if any, on your target machine. If there is no instruction cache, this subroutine may be a no-op.

On target machines that have instruction caches, [GDB] requires this function to make certain that the state of your program is stable.

You must also make sure this library routine is available:

`void *memset(void *, int, int)`

This is the standard library function `memset` that sets an area of memory to a known value. If you have one of the free versions of `libc.a`, `memset` can be found there; otherwise, you must either obtain it from your hardware manufacturer, or write your own.

If you do not use the GNU C compiler, you may need other standard library subroutines as well; this varies from one stub to another, but in general the stubs are likely to use any of the common library subroutines which `GCC` generates as inline code.

---

::: header
Next: [Debug Session](Debug-Session.html#Debug-Session)]
:::
