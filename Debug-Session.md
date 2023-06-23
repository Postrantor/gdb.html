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

1. Make sure you have defined the supporting low-level routines (see [What You Must Do for the Stub](Bootstrapping.html#Bootstrapping)):

   ::: display

   ```display
   getDebugChar, putDebugChar,
   flush_i_cache, memset, exceptionHandler.
   ```

   :::
2. Insert these lines in your program's startup code, before the main procedure is called:

   ::: smallexample

   ```bash
   set_debug_traps();
   breakpoint();
   ```

   :::

   On some machines, when a breakpoint trap is raised, the hardware automatically makes the PC point to the instruction after the breakpoint. If your machine doesn't do that, you may need to adjust `handle_exception` to arrange for it to return to the instruction after the breakpoint on this first invocation, so that your program doesn't keep hitting the initial breakpoint instead of making progress.
3. For the 680x0 stub only, you need to provide a variable called `exceptionHook`. Normally you just use:

   ::: smallexample

   ```bash
   void (*exceptionHook)() = 0;
   ```

   :::

   but if before calling `set_debug_traps`, you set it to point to a function in your program, that function is called when `GDB` continues after stopping on a trap (for example, bus error). The function indicated by `exceptionHook` is called with one parameter: an `int` which is the exception number.
4. Compile and link together: your program, the [GDB] debugging stub for your target architecture, and the supporting subroutines.
5. Make sure you have a serial connection between your target machine and the [GDB] host, and identify the serial port on the host.
6. Download your program to your target machine (or get it there by whatever means the manufacturer provides), and start it.
7. Start [GDB] on the host, and connect to the target (see [Connecting to a Remote Target](Connecting.html#Connecting)).

---

::: header
Previous: [Bootstrapping](Bootstrapping.html#Bootstrapping)]
:::
