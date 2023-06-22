---
description: Attach (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Attach (Debugging with GDB)
lang: en
resource-type: document
title: Attach (Debugging with GDB)
---
::: header
Next: [Kill Process](Kill-Process.html#Kill-Process)]
:::

---

### 4.7 Debugging an Already-running Process

`attach process-id`

:   This command attaches to a running process---one that was started outside [GDB]' shell command.

```
`attach` does not repeat if you press RET a second time after executing the command.
```

To use `attach`, your program must be running in an environment which supports processes; for example, `attach` does not work for programs on bare-board targets that lack an operating system. You must also have permission to send the process a signal.

When you use `attach`, the debugger finds the program running in the process first by looking in the current working directory, then (if the program is not found) by using the source file search path (see [Specifying Source Directories](Source-Path.html#Source-Path)). You can also use the `file` command to load the program. See [Commands to Specify Files](Files.html#Files).

If the debugger can determine that the executable file running in the process it is attaching to does not match the current exec-file loaded by [GDB] tries to compare the files by comparing their build IDs (see [build ID](Separate-Debug-Files.html#build-ID)), if available.

`set exec-file-mismatch ‘ask|warn|off’`

Whether to detect mismatch between the current executable file loaded by [GDB]', don't attempt to detect a mismatch. If the user confirms loading the process executable file, then its symbols will be loaded as well.

`show exec-file-mismatch`

Show the current value of `exec-file-mismatch`.

The first thing [GDB] to the process.

`detach`

When you have finished debugging the attached process, you can use the `detach` command to release it from [GDB] become completely independent once more, and you are ready to `attach` another process or start one with `run`. `detach` does not repeat if you press RET again after executing the command.

If you exit [GDB] asks for confirmation if you try to do either of these things; you can control whether or not you need to confirm by using the `set confirm` command (see [Optional Warnings and Messages](Messages_002fWarnings.html#Messages_002fWarnings)).

---

::: header
Next: [Kill Process](Kill-Process.html#Kill-Process)]
:::
