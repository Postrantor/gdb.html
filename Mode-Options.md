---
description: Mode Options (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Mode Options (Debugging with GDB)
lang: en
resource-type: document
title: Mode Options (Debugging with GDB)
---
::: header
Next: [Startup](Startup.html#Startup)]
:::

---

#### 2.1.2 Choosing Modes

You can run [GDB] in various alternative modes---for example, in batch mode or quiet mode.

`-nx`

`-n`

Do not execute commands found in any initialization files (see [Initialization Files](Initialization-Files.html#Initialization-Files)).

`-nh`

Do not execute commands found in any home directory initialization file (see [Home directory initialization file](Initialization-Files.html#Initialization-Files)). The system wide and current directory initialization files are still loaded.

`-quiet`

`-silent`

`-q`

"Quiet". Do not print the introductory and copyright messages. These messages are also suppressed in batch mode.

This can also be enabled using `set startup-quietly on`. The default is `off`. Use `show startup-quietly` to see the current setting. Place `set startup-quietly on` into your early initialization file (see [Initialization Files](Initialization-Files.html#Initialization-Files)) to have future [GDB] sessions startup quietly.

`-batch`

Run in batch mode. Exit with status `0` after processing all the command files specified with '`-x` were in effect (see [Messages/Warnings](Messages_002fWarnings.html#Messages_002fWarnings)).

Batch mode may be useful for running [GDB] as a filter, for example to download and run a program on another computer; in order to make this more useful, the message

::: smallexample

```bash
Program exited normally.
```

:::

(which is ordinarily issued whenever a program running under [GDB] control terminates) is not issued when running in batch mode.

`-batch-silent`

Run in batch mode exactly like '`-batch`' and would be useless for an interactive session.

This is particularly useful when using targets that give '`Loading section`' messages, for example.

Note that targets that give their output via [GDB], as opposed to writing directly to `stdout`, will also be made silent.

`-return-child-result`

The return code from [GDB] will be the return code from the child process (the process being debugged), with the following exceptions:

- [GDB]'.
- The user quits with an explicit value. E.g., '`quit 1`'.
- The child process never runs, or is not allowed to terminate, in which case the exit code will be -1.

This option is useful in conjunction with '`-batch` is being used as a remote program loader or simulator interface.

`-nowindows`

`-nw`

"No windows". If [GDB] to only use the command-line interface. If no GUI is available, this option has no effect.

`-windows`

`-w`

If [GDB] includes a GUI, then this option requires it to be used if possible.

`-cd directory`

Run [GDB] as its working directory, instead of the current directory.

`-data-directory directory`

`-D directory`

Run [GDB] searches for its auxiliary files. See [Data Files](Data-Files.html#Data-Files).

`-fullname`

`-f`

[GNU]' characters as a signal to display the source code for the frame.

`-annotate level`

This option sets the *annotation level* inside [GDB], and level 2 has been deprecated.

The annotation mechanism has largely been superseded by [GDB/MI] (see [GDB/MI](GDB_002fMI.html#GDB_002fMI)).

`--args`

Change interpretation of command line so that arguments following the executable file are passed as command line arguments to the inferior. This option stops option processing.

`-baud bps`

`-b bps`

Set the line speed (baud rate or bits per second) of any serial interface used by [GDB] for remote debugging.

`-l timeout`

Set the timeout (in seconds) of any communication used by [GDB] for remote debugging.

`-tty device`

`-t device`

Run using `device` for your program's standard input and output.

`-tui`

Activate the *Text User Interface* when starting. The Text User Interface manages several text windows on the terminal, showing source, assembly, registers and [GDB] Emacs](Emacs.html#Emacs)).

`-interpreter interp`

Use the interpreter `interp` using it as a back end. See [Command Interpreters](Interpreters.html#Interpreters).

'`--interpreter=mi` interfaces are no longer supported.

`-write`

Open the executable and core files for both reading and writing. This is equivalent to the '`set write on` (see [Patching](Patching.html#Patching)).

`-statistics`

This option causes [GDB] to print statistics about time and memory usage after it completes each command and returns to the prompt.

`-version`

This option causes [GDB] to print its version number and no-warranty blurb, and exit.

`-configuration`

This option causes [GDB] bugs (see [GDB Bugs](GDB-Bugs.html#GDB-Bugs)).

---

::: header
Next: [Startup](Startup.html#Startup)]
:::
