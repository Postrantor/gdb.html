---
description: Cygwin Native (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Cygwin Native (Debugging with GDB)
lang: en
resource-type: document
title: Cygwin Native (Debugging with GDB)
---
::: header
Next: [Hurd Native](Hurd-Native.html#Hurd-Native)]
:::

---

#### 21.1.4 Features for Debugging MS Windows PE Executables

[GDB] supports native debugging of MS Windows programs, including DLLs with and without symbolic debugging information.

MS-Windows programs that call `SetConsoleMode` to switch off the special meaning of the '`Ctrl-C`.

There are various additional Cygwin-specific commands, described in this section. Working with DLLs that have no debugging symbols is described in [Non-debug DLL Symbols](Non_002ddebug-DLL-Symbols.html#Non_002ddebug-DLL-Symbols).

`info w32`

This is a prefix of MS Windows-specific commands which print information about the target system and important OS structures.

`info w32 selector`

This command displays information returned by the Win32 API `GetThreadSelectorEntry` function. It takes an optional argument that is evaluated to a long value to give the information about this given selector. Without argument, this command displays information about the six segment registers.

`info w32 thread-information-block`

This command displays thread specific information stored in the Thread Information Block (readable on the X86 CPU family using `$fs` selector for 32-bit programs and `$gs` for 64-bit programs).

`signal-event id`

This command signals an event with user-provided `id`. Used to resume crashing process when attached to it using MS-Windows JIT debugging (AeDebug).

To use it, create or edit the following keys in `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug` and/or `HKLM\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug` (for x86_64 versions):

- \- `Debugger` (REG_SZ) --- a command to launch the debugger. Suggested command is: `fully-qualified-path-to-gdb.exe -ex "attach %ld" -ex "signal-event %ld" -ex "continue"`.

  The first `%ld` will be replaced by the process ID of the crashing process, the second `%ld` will be replaced by the ID of the event that blocks the crashing process, waiting for [GDB] to attach.
- \- `Auto` (REG_SZ) --- either `1` or `0`. `1` will make the system run debugger specified by the Debugger key automatically, `0` will cause a dialog box with "OK" and "Cancel" buttons to appear, which allows the user to either terminate the crashing process (OK) or debug it (Cancel).

`set cygwin-exceptions mode`

If `mode` users with false `SIGSEGV` signals.

`show cygwin-exceptions`

Displays whether [GDB] will break on exceptions that happen inside the Cygwin DLL itself.

`set new-console mode`

If `mode` is `off`, the debuggee will be started in the same console as the debugger.

`show new-console`

Displays whether a new console is used when the debuggee is started.

`set new-group mode`

This boolean value controls whether the debuggee should start a new group or stay in the same group as the debugger. This affects the way the Windows OS handles '`Ctrl-C`'.

`show new-group`

Displays current value of new-group boolean.

`set debugevents`

This boolean value adds debug output concerning kernel events related to the debuggee seen by the debugger. This includes events that signal thread and process creation and exit, DLL loading and unloading, console interrupts, and debugging messages produced by the Windows `OutputDebugString` API call.

`set debugexec`

This boolean value adds debug output concerning execute events (such as resume thread) seen by the debugger.

`set debugexceptions`

This boolean value adds debug output concerning exceptions in the debuggee seen by the debugger.

`set debugmemory`

This boolean value adds debug output concerning debuggee memory reads and writes by the debugger.

`set shell`

This boolean values specifies whether the debuggee is called via a shell or directly (default value is on).

`show shell`

Displays if the debuggee will be started with a shell.

---

• [Non-debug DLL Symbols](Non_002ddebug-DLL-Symbols.html#Non_002ddebug-DLL-Symbols):        Support for DLLs without debugging symbols

---

---

::: header
Next: [Hurd Native](Hurd-Native.html#Hurd-Native)]
:::
