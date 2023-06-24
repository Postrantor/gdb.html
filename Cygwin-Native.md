---
tip: translate by openai@2023-06-23 20:08:41
...
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

> [GDB]支持对包括有和没有符号调试信息的MS Windows程序的本机调试，包括DLL。


MS-Windows programs that call `SetConsoleMode` to switch off the special meaning of the '`Ctrl-C`.

> 程序调用`SetConsoleMode`来关闭'Ctrl-C'的特殊含义，这是MS-Windows程序。


There are various additional Cygwin-specific commands, described in this section. Working with DLLs that have no debugging symbols is described in [Non-debug DLL Symbols](Non_002ddebug-DLL-Symbols.html#Non_002ddebug-DLL-Symbols).

> 在本节中描述了各种额外的Cygwin特定命令。处理没有调试符号的DLL的方法可参见[Non-debug DLL Symbols](Non_002ddebug-DLL-Symbols.html#Non_002ddebug-DLL-Symbols)。

`info w32`


This is a prefix of MS Windows-specific commands which print information about the target system and important OS structures.

> 这是一个MS Windows特定命令的前缀，用于打印有关目标系统和重要操作系统结构的信息。

`info w32 selector`


This command displays information returned by the Win32 API `GetThreadSelectorEntry` function. It takes an optional argument that is evaluated to a long value to give the information about this given selector. Without argument, this command displays information about the six segment registers.

> 这个命令显示Win32 API函数`GetThreadSelectorEntry`返回的信息。它接受一个可选参数，该参数被评估为长值，以给出关于给定选择器的信息。如果没有参数，此命令将显示关于六个段寄存器的信息。

`info w32 thread-information-block`


This command displays thread specific information stored in the Thread Information Block (readable on the X86 CPU family using `$fs` selector for 32-bit programs and `$gs` for 64-bit programs).

> 这个命令显示存储在线程信息块（在X86 CPU家族中使用32位程序的$fs选择器和64位程序的$gs可读）中的特定线程信息。

`signal-event id`


This command signals an event with user-provided `id`. Used to resume crashing process when attached to it using MS-Windows JIT debugging (AeDebug).

> 这个命令使用用户提供的ID来信号一个事件。当使用MS-Windows JIT调试（AeDebug）附加时，用于恢复崩溃进程。


To use it, create or edit the following keys in `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug` and/or `HKLM\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug` (for x86_64 versions):

> 要使用它，请在`HKLM \ SOFTWARE \ Microsoft \ Windows NT \ CurrentVersion \ AeDebug`和/或`HKLM \ SOFTWARE \ Wow6432Node \ Microsoft \ Windows NT \ CurrentVersion \ AeDebug`（针对x86_64版本）中创建或编辑以下键：


- \- `Debugger` (REG_SZ) --- a command to launch the debugger. Suggested command is: `fully-qualified-path-to-gdb.exe -ex "attach %ld" -ex "signal-event %ld" -ex "continue"`.

> 调试器（REG_SZ）--- 启动调试器的命令。建议的命令是：`完整路径-to-gdb.exe -ex "attach %ld" -ex "signal-event %ld" -ex "continue"`。


  The first `%ld` will be replaced by the process ID of the crashing process, the second `%ld` will be replaced by the ID of the event that blocks the crashing process, waiting for [GDB] to attach.

> 第一个`%ld`将被崩溃进程的进程ID所替换，第二个`%ld`将被阻止崩溃进程的事件ID所替换，等待[GDB]连接。

- \- `Auto` (REG_SZ) --- either `1` or `0`. `1` will make the system run debugger specified by the Debugger key automatically, `0` will cause a dialog box with "OK" and "Cancel" buttons to appear, which allows the user to either terminate the crashing process (OK) or debug it (Cancel).

> `- \- `自动` (REG_SZ) --- 可以是`1`或`0`。`1`会自动运行由Debugger键指定的调试器，`0`会出现一个带有“确定”和“取消”按钮的对话框，用户可以选择终止崩溃进程（确定）或调试它（取消）。

`set cygwin-exceptions mode`

If `mode` users with false `SIGSEGV` signals.

`show cygwin-exceptions`


Displays whether [GDB] will break on exceptions that happen inside the Cygwin DLL itself.

> 显示GDB是否会在Cygwin DLL本身中发生的异常上中断。

`set new-console mode`


If `mode` is `off`, the debuggee will be started in the same console as the debugger.

> 如果mode为off，被调试对象将在与调试器相同的控制台中启动。

`show new-console`

Displays whether a new console is used when the debuggee is started.

`set new-group mode`


This boolean value controls whether the debuggee should start a new group or stay in the same group as the debugger. This affects the way the Windows OS handles '`Ctrl-C`'.

> 这个布尔值控制调试者是否应该开始一个新组，或者和调试者保持在同一组中。这会影响Windows操作系统处理`Ctrl-C`的方式。

`show new-group`

Displays current value of new-group boolean.

`set debugevents`


This boolean value adds debug output concerning kernel events related to the debuggee seen by the debugger. This includes events that signal thread and process creation and exit, DLL loading and unloading, console interrupts, and debugging messages produced by the Windows `OutputDebugString` API call.

> 这个布尔值增加了调试器看到的与调试对象相关的内核事件的调试输出。这包括信号线程和进程创建和退出、DLL加载和卸载、控制台中断以及由Windows的`OutputDebugString` API调用产生的调试消息。

`set debugexec`


This boolean value adds debug output concerning execute events (such as resume thread) seen by the debugger.

> 此布尔值添加有关调试器所看到的执行事件（如恢复线程）的调试输出。

`set debugexceptions`


This boolean value adds debug output concerning exceptions in the debuggee seen by the debugger.

> 这个布尔值增加了调试器看到的调试者中关于异常的调试输出。

`set debugmemory`


This boolean value adds debug output concerning debuggee memory reads and writes by the debugger.

> 这个布尔值增加了有关调试器对调试目标内存读写的调试输出。

`set shell`


This boolean values specifies whether the debuggee is called via a shell or directly (default value is on).

> 这个布尔值指定调试对象是通过shell调用还是直接调用（默认值为开启）。

`show shell`

Displays if the debuggee will be started with a shell.

---


• [Non-debug DLL Symbols](Non_002ddebug-DLL-Symbols.html#Non_002ddebug-DLL-Symbols):        Support for DLLs without debugging symbols

> • [非调试 DLL 符号](Non_002ddebug-DLL-Symbols.html#Non_002ddebug-DLL-Symbols):        支持没有调试符号的 DLL。

---

---

::: header
Next: [Hurd Native](Hurd-Native.html#Hurd-Native)]
:::
