---
description: Dynamic Printf (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Dynamic Printf (Debugging with GDB)
lang: en
resource-type: document
title: Dynamic Printf (Debugging with GDB)
---
::: header
Next: [Save Breakpoints](Save-Breakpoints.html#Save-Breakpoints)]
:::

---

#### 5.1.8 Dynamic Printf

The dynamic printf command `dprintf` combines a breakpoint with formatted printing of your program's data to give you the effect of inserting `printf` calls into your program on-the-fly, without having to recompile it.

In its most basic form, the output goes to the GDB console. However, you can set the variable `dprintf-style` for alternate handling. For instance, you can ask to format the output by calling your program's `printf` function. This has the advantage that the characters go to the program's output device, so they can recorded in redirects to files and so forth.

If you are doing remote debugging with a stub or agent, you can also ask to have the printf handled by the remote agent. In addition to ensuring that the output goes to the remote program's device along with any other output the program might produce, you can also ask that the dprintf remain active even after disconnecting from the remote target. Using the stub/agent is also more efficient, as it can do everything without needing to communicate with [GDB].

`dprintf locspec,template,expression[,expression…]`

Whenever execution reaches a code location that results from resolving `locspec`. To print several values, separate them with commas.

`set dprintf-style style`

Set the dprintf output to be handled in one of several different styles enumerated below. A change of style affects all existing dynamic printfs immediately. (If you need individual control over the print commands, simply define normal breakpoints with explicitly-supplied command lists.)

`gdb`

:

```
Handle the output using the [GDB]' format specifier (see [%V Format Specifier](Output.html#g_t_0025V-Format-Specifier)).
```

`call`

:

```
Handle the output by calling a function in your program (normally `printf`). When using this style the supported format specifiers depend entirely on the function being called.

Most of [GDB]' style dprintf, care should be taken to ensure that only format specifiers supported by the output function are used, otherwise the results will be undefined.
```

`agent`

:

```
Have the remote debugging agent (such as `gdbserver`) handle the output itself. This style is only available for agents that support running commands on the target. This style does not support the '`%V`' format specifier.
```

`set dprintf-function function`

Set the function to call if the dprintf style is `call`. By default its value is `printf`. You may set it to any expression that [GDB] can evaluate to a function, as per the `call` command.

`set dprintf-channel channel`

Set a "channel" for dprintf. If set to a non-empty value, [GDB] will evaluate it as an expression and pass the result as a first argument to the `dprintf-function`, in the manner of `fprintf` and similar functions. Otherwise, the dprintf format string will be the first argument, in the manner of `printf`.

As an example, if you wanted `dprintf` output to go to a logfile that is a standard I/O stream assigned to the variable `mylog`, you could do the following:

::: example

```example
(gdb) set dprintf-style call
(gdb) set dprintf-function fprintf
(gdb) set dprintf-channel mylog
(gdb) dprintf 25,"at line 25, glob=%d\n",glob
Dprintf 1 at 0x123456: file main.c, line 25.
(gdb) info break
1       dprintf        keep y   0x00123456 in main at main.c:25
        call (void) fprintf (mylog,"at line 25, glob=%d\n",glob)
        continue
(gdb)
```

:::

Note that the `info break` displays the dynamic printf commands as normal breakpoint commands; you can thus easily see the effect of the variable settings.

`set disconnected-dprintf on`

`set disconnected-dprintf off`

Choose whether `dprintf` commands should continue to run if [GDB] has disconnected from the target. This only applies if the `dprintf-style` is `agent`.

`show disconnected-dprintf off`

Show the current choice for disconnected `dprintf`.

[GDB] will report an error.

---

::: header
Next: [Save Breakpoints](Save-Breakpoints.html#Save-Breakpoints)]
:::
