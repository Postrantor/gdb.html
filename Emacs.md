---
description: Emacs (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Emacs (Debugging with GDB)
lang: en
resource-type: document
title: Emacs (Debugging with GDB)
---
::: header
Next: [GDB/MI](GDB_002fMI.html#GDB_002fMI)]
:::

---

## 26 Using [GDB]

A special interface allows you to use [GNU].

To use this interface, use the command [M-x gdb] as a subprocess of Emacs, with input and output through a newly created Emacs buffer.

Running [GDB] normally except for two things:

- All "terminal" input and output goes through an Emacs buffer, called the GUD buffer.

  This applies both to [GDB] commands and their output, and to the input and output done by the program you are debugging.

  This is useful because it means that you can copy the text of previous commands and input them again; you can even use parts of the output in this way.

  All the facilities of Emacs' Shell mode are available for interacting with your program. In particular, you can send signals the usual way---for example, [C-c C-c] for a stop.
- [GDB] displays source code through Emacs.

  Each time [GDB] session and the source.

  Explicit [GDB] `list` or search commands still produce output as usual, but you probably have no reason to use them from Emacs.

We call this *text command mode*. Emacs 22.1, and later, also uses a graphical mode, enabled by default, which provides further buffers that can control the execution and describe the state of your program. See [GDB Graphical Interface](../Emacs/GDB-Graphical-Interface.html#GDB-Graphical-Interface) in The [GNU] Emacs Manual.

If you specify an absolute file name when prompted for the [M-x gdb] input and output session proceeds normally, the auxiliary buffer does not display the current source and line of execution.

The initial working directory of [GDB] to operate on. See [Commands to Specify Files](Files.html#Files).

By default, [M-x gdb] by a different name (for example, if you keep several configurations around, with different names) you can customize the Emacs variable `gud-gdb-command-name` to run the one you want.

In the GUD buffer, you can use these special Emacs commands in addition to the standard Shell mode commands:

[C-h m]

:   Describe the features of Emacs' GUD Mode.

[C-c C-s]

:   Execute to another source line, like the [GDB] `step` command; also update the display window to show the current file and location.

[C-c C-n]

:   Execute to next source line in this function, skipping all function calls, like the [GDB] `next` command. Then update the display window to show the current file and location.

[C-c C-i]

:   Execute one instruction, like the [GDB] `stepi` command; update display window accordingly.

[C-c C-f]

:   Execute until exit from the selected stack frame, like the [GDB] `finish` command.

[C-c C-r]

:   Continue execution of your program, like the [GDB] `continue` command.

[C-c \<]

:   Go up the number of frames indicated by the numeric argument (see [Numeric Arguments](../Emacs/Arguments.html#Arguments) in The [GNU] `up` command.

[C-c \>]

:   Go down the number of frames indicated by the numeric argument, like the [GDB] `down` command.

In any source file, the Emacs command [C-x [SPC] to set a breakpoint on the source line point is on.

In text command mode, if you type [M-x speedbar] to make the selected frame become the current one. In graphical mode, the speedbar displays watch expressions.

If you accidentally delete the source-display buffer, an easy way to get it back is to type the command `f` in the [GDB] buffer, to request a frame display; when you run under Emacs, this recreates the source buffer if necessary to show you the context of the current frame.

The source files displayed in Emacs are in ordinary Emacs buffers which are visiting the source files in the usual way. You can edit the files with these buffers if you wish; but keep in mind that [GDB] knows cease to correspond properly with the code.

A more detailed description of Emacs' interaction with [GDB] Emacs Manual).

---

::: header
Next: [GDB/MI](GDB_002fMI.html#GDB_002fMI)]
:::
