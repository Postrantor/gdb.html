---
tip: translate by openai@2023-06-23 20:22:00
...
---
description: Debugging Output (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Debugging Output (Debugging with GDB)
lang: en
resource-type: document
title: Debugging Output (Debugging with GDB)
---
::: header
Next: [Other Misc Settings](Other-Misc-Settings.html#Other-Misc-Settings)]
:::

---

### 22.10 Optional Messages about Internal Happenings


[GDB] maintainers, or when reporting a bug. This section documents those commands.

> [GDB] 维护者，或者在报告错误时。本节记录了这些命令。

`set exec-done-display`


Turns on or off the notification of asynchronous commands' completion. When on, [GDB]

> 开启或关闭异步命令完成的通知。 开启时，[GDB]

`show exec-done-display`


Displays the current setting of asynchronous command completion notification.

> 顯示當前異步命令完成通知的設置。

`set debug aarch64`


Turns on or off display of debugging messages related to ARM AArch64. The default is off.

> 开启或关闭与ARM AArch64相关的调试消息的显示。默认关闭。

`show debug aarch64`


Displays the current state of displaying debugging messages related to ARM AArch64.

> 顯示與ARM AArch64相關的偵錯訊息的目前狀態。

`set debug arch`

Turns on or off display of gdbarch debugging info. The default is off

`show debug arch`

Displays the current state of displaying gdbarch debugging info.

`set debug aix-thread`

Display debugging messages about inner workings of the AIX thread module.

`show debug aix-thread`

Show the current state of AIX thread debugging info display.

`set debug amd-dbgapi-lib`

`show debug amd-dbgapi-lib`


The `set debug amd-dbgapi-lib log-level level` command can be used to enable diagnostic messages from the '`amd-dbgapi` can be:

> 命令`set debug amd-dbgapi-lib log-level level`可用于启用来自'amd-dbgapi'的诊断消息。

`off`

:   no logging is enabled

`error`

:   fatal errors are reported

`warning`

:   fatal errors and warnings are reported

`info`

:   fatal errors, warnings, and info messages are reported

`verbose`

:   all messages are reported


The `show debug amd-dbgapi-lib log-level` command displays the current amd-dbgapi library log level.

> 命令`show debug amd-dbgapi-lib log-level`显示当前amd-dbgapi库的日志级别。

`set debug amd-dbgapi`

`show debug amd-dbgapi`


The '`set debug amd-dbgapi`' command displays the current setting. See [set debug amd-dbgapi](#set-debug-amd_002ddbgapi).

> 命令`set debug amd-dbgapi`显示当前设置。请参见[set debug amd-dbgapi](#set-debug-amd_002ddbgapi)。

`set debug check-physname`


Check the results of the "physname" computation. When reading DWARF debugging information for C++, [GDB] to compute the names both ways and display any discrepancies.

> 检查"physname"计算的结果。当读取C++的DWARF调试信息时，使用GDB两种方式计算名称并显示任何差异。

`show debug check-physname`

Show the current state of "physname" checking.

`set debug coff-pe-read`


Control display of debugging messages related to reading of COFF/PE exported symbols. The default is off.

> 控制调试消息的显示，与读取COFF/PE导出符号有关。默认是关闭的。

`show debug coff-pe-read`


Displays the current state of displaying debugging messages related to reading of COFF/PE exported symbols.

> 显示与读取COFF/PE导出符号相关的调试消息的当前状态。

`set debug dwarf-die`


Dump DWARF DIEs after they are read in. The value is the number of nesting levels to print. A value of zero turns off the display.

> 在读取后将DWARF DIE转储。值为要打印的嵌套级别的数量。值为零会关闭显示。

`show debug dwarf-die`

Show the current state of DWARF DIE debugging.

`set debug dwarf-line`


Turns on or off display of debugging messages related to reading DWARF line tables. The default is 0 (off). A value of 1 provides basic information. A value greater than 1 provides more verbose information.

> 开启或关闭与读取DWARF行表相关的调试消息的显示。默认值为0（关闭）。值为1时提供基本信息。值大于1时提供更详细的信息。

`show debug dwarf-line`

Show the current state of DWARF line table debugging.

`set debug dwarf-read`


Turns on or off display of debugging messages related to reading DWARF debug info. The default is 0 (off). A value of 1 provides basic information. A value greater than 1 provides more verbose information.

> 开启或关闭显示与读取DWARF调试信息相关的调试消息。默认值为0（关闭）。值为1时提供基本信息。大于1的值提供更详细的信息。

`show debug dwarf-read`

Show the current state of DWARF reader debugging.

`set debug displaced`


Turns on or off display of [GDB] debugging info for the displaced stepping support. The default is off.

> 开启或关闭[GDB]对位移步进支持的调试信息显示。默认为关闭。

`show debug displaced`


Displays the current state of displaying [GDB] debugging info related to displaced stepping.

> 显示与位移步进相关的[GDB]调试信息的当前状态。

`set debug event`


Turns on or off display of [GDB] event debugging info. The default is off.

> 开启或关闭[GDB]事件调试信息的显示。默认情况下是关闭的。

`show debug event`

Displays the current state of displaying [GDB] event debugging info.

`set debug event-loop`


Controls output of debugging info about the event loop. The possible values are '`off`' (shows all debugging info except those about UI-related events).

> 控制有关事件循环的调试信息的输出。可能的值为'off'(显示所有调试信息，但不显示与UI相关的事件)。

`show debug event-loop`


Shows the current state of displaying debugging info about the event loop.

> 显示有关事件循环的调试信息的当前状态。

`set debug expression`


Turns on or off display of debugging info about [GDB] expression parsing. The default is off.

> 开启或关闭关于[GDB]表达式解析的调试信息显示。默认关闭。

`show debug expression`


Displays the current state of displaying debugging info about [GDB] expression parsing.

> 显示有关[GDB]表达式解析的调试信息的当前状态。

`set debug fbsd-lwp`

Turns on or off debugging messages from the FreeBSD LWP debug support.

`show debug fbsd-lwp`

Show the current state of FreeBSD LWP debugging messages.

`set debug fbsd-nat`

Turns on or off debugging messages from the FreeBSD native target.

`show debug fbsd-nat`

Show the current state of FreeBSD native target debugging messages.

`set debug fortran-array-slicing`


Turns on or off display of [GDB] Fortran array slicing debugging info. The default is off.

> 开启或关闭[GDB] Fortran数组切片调试信息的显示。默认是关闭的。

`show debug fortran-array-slicing`


Displays the current state of displaying [GDB] Fortran array slicing debugging info.

> 顯示[GDB] Fortran陣列切片調試資訊的當前狀態。

`set debug frame`


Turns on or off display of [GDB] frame debugging info. The default is off.

> 开启或关闭[GDB]帧调试信息的显示。默认情况下是关闭的。

`show debug frame`

Displays the current state of displaying [GDB] frame debugging info.

`set debug gnu-nat`

Turn on or off debugging messages from the [GNU]/Hurd debug support.

`show debug gnu-nat`

Show the current state of [GNU]/Hurd debugging messages.

`set debug infrun`


Turns on or off display of [GDB] contains GDB's runtime state machine used for implementing operations such as single-stepping the inferior.

> 打开或关闭[GDB]的显示，其中包含GDB的运行时状态机，用于实现诸如单步执行次级程序等操作。

`show debug infrun`

Displays the current state of [GDB] inferior debugging.

`set debug infcall`


Turns on or off display of debugging info related to inferior function calls made by [GDB].

> 打开或关闭[GDB]调用的次级函数的调试信息的显示。

`show debug infcall`

Displays the current state of [GDB] inferior function call debugging.

`set debug jit`

Turn on or off debugging messages from JIT debug support.

`show debug jit`

Displays the current state of [GDB] JIT debugging.

`set debug linux-nat [on|off]`


Turn on or off debugging messages from the Linux native target debug support.

> 开启或关闭来自Linux本地目标调试支持的调试消息。

`show debug linux-nat`

Show the current state of Linux native target debugging messages.

`set debug linux-namespaces`


Turn on or off debugging messages from the Linux namespaces debug support.

> 开启或关闭来自Linux名称空间调试支持的调试消息。

`show debug linux-namespaces`

Show the current state of Linux namespaces debugging messages.

`set debug mach-o`


Control display of debugging messages related to Mach-O symbols processing. The default is off.

> 控制与Mach-O符号处理相关的调试消息的显示。默认为关闭。

`show debug mach-o`


Displays the current state of displaying debugging messages related to reading of COFF/PE exported symbols.

> 显示有关读取COFF/PE导出符号的调试消息的当前状态。

`set debug notification`


Turn on or off debugging messages about remote async notification. The default is off.

> 关闭或打开有关远程异步通知的调试消息。默认情况下关闭。

`show debug notification`


Displays the current state of remote async notification debugging messages.

> 显示远程异步通知调试消息的当前状态。

`set debug observer`


Turns on or off display of [GDB] observer debugging. This includes info such as the notification of observable events.

> 开启或关闭[GDB]观察调试的显示。这包括可观察事件的通知等信息。

`show debug observer`

Displays the current state of observer debugging.

`set debug overload`


Turns on or off display of [GDB] C++ overload debugging info. This includes info such as ranking of functions, etc. The default is off.

> 开启或关闭[GDB] C++重载调试信息的显示。这包括函数排名等信息。默认是关闭的。

`show debug overload`


Displays the current state of displaying [GDB] C++ overload debugging info.

> 显示[GDB] C++重载调试信息的当前状态。

`set debug parser`


Turns on or off the display of expression parser debugging output. Internally, this sets the `yydebug` variable in the expression parser. See [Tracing Your Parser](http://www.gnu.org/software/bison/manual/html_node/Tracing.html#Tracing) in Bison, for details. The default is off.

> 开启或关闭表达式解析器调试输出的显示。在内部，这会设置表达式解析器中的`yydebug`变量。有关详细信息，请参阅Bison中的[跟踪您的解析器](http://www.gnu.org/software/bison/manual/html_node/Tracing.html#Tracing)。默认情况下是关闭的。

`show debug parser`

Show the current state of expression parser debugging.

`set debug remote`


Turns on or off display of reports on all packets sent back and forth across the serial line to the remote machine. The info is printed on the [GDB] standard output stream. The default is off.

> 打开或关闭显示发送到远程机器的串行线路上来回发送的所有报告。信息打印在[GDB]标准输出流上。默认情况下是关闭的。

`show debug remote`

Displays the state of display of remote packets.

`set debug remote-packet-max-chars`


Sets the maximum number of characters to display for each remote packet when `set debug remote` is on. This is useful to prevent [GDB] from displaying lengthy remote packets and polluting the console.

> 设置在`set debug remote`开启时，每个远程数据包显示的最大字符数。这有助于防止[GDB]显示冗长的远程数据包，从而污染控制台。


The default value is `512`, which means [GDB] will truncate each remote packet after 512 bytes.

> 默认值为`512`，这意味着[GDB]会在每个远程数据包达到512字节后截断它们。


Setting this option to `unlimited` will disable truncation and will output the full length of the remote packets.

> 将此选项设置为“无限”将禁用截断，并输出远程数据包的完整长度。

`show debug remote-packet-max-chars`

Displays the number of bytes to output for remote packet debugging.

`set debug separate-debug-file`

Turns on or off display of debug output about separate debug file search.

`show debug separate-debug-file`

Displays the state of separate debug file search debug output.

`set debug serial`


Turns on or off display of [GDB] serial debugging info. The default is off.

> 关闭或打开[GDB]串口调试信息的显示。默认情况下是关闭的。

`show debug serial`

Displays the current state of displaying [GDB] serial debugging info.

`set debug solib`


Turns on or off display of debugging messages related to shared libraries. The default is off.

> 开启或关闭显示与共享库相关的调试消息。默认情况下是关闭的。

`show debug solib`

Show the current state of solib debugging messages.

`set debug symbol-lookup`


Turns on or off display of debugging messages related to symbol lookup. The default is 0 (off). A value of 1 provides basic information. A value greater than 1 provides more verbose information.

> 开启或关闭与符号查找相关的调试消息的显示。默认值为0（关闭）。值为1提供基本信息。大于1的值提供更多详细信息。

`show debug symbol-lookup`

Show the current state of symbol lookup debugging messages.

`set debug symfile`


Turns on or off display of debugging messages related to symbol file functions. The default is off. See [Files](Files.html#Files).

> 打开或关闭与符号文件功能相关的调试消息的显示。默认情况下是关闭的。请参阅[文件](Files.html#Files)。

`show debug symfile`

Show the current state of symbol file debugging messages.

`set debug symtab-create`


Turns on or off display of debugging messages related to symbol table creation. The default is 0 (off). A value of 1 provides basic information. A value greater than 1 provides more verbose information.

> 开启或关闭与符号表创建相关的调试消息的显示。默认为0（关闭）。值为1时提供基本信息。大于1的值提供更详细的信息。

`show debug symtab-create`

Show the current state of symbol table creation debugging.

`set debug target`


Turns on or off display of [GDB] target debugging info. This info includes what is going on at the target level of GDB, as it happens. The default is 0. Set it to 1 to track events, and to 2 to also track the value of large memory transfers.

> 开启或关闭[GDB]目标调试信息的显示。此信息包括GDB目标层面上发生的事情。默认值为0。将其设置为1以跟踪事件，将其设置为2以跟踪大型内存传输的值。

`show debug target`

Displays the current state of displaying [GDB] target debugging info.

`set debug timestamp`


Turns on or off display of timestamps with [GDB] debugging info. When enabled, seconds and microseconds are displayed before each debugging message.

> 开启或关闭 [GDB] 调试信息的时间戳显示。 启用时，每条调试消息前会显示秒和微秒。

`show debug timestamp`


Displays the current state of displaying timestamps with [GDB] debugging info.

> 显示[GDB]调试信息中当前时间戳的显示状态。

`set debug varobj`


Turns on or off display of [GDB] variable object debugging info. The default is off.

> 开启或关闭 [GDB] 变量对象调试信息的显示。默认情况下是关闭的。

`show debug varobj`


Displays the current state of displaying [GDB] variable object debugging info.

> 显示[GDB]变量对象调试信息的当前状态。

`set debug xml`

Turn on or off debugging messages for built-in XML parsers.

`show debug xml`

Displays the current state of XML debugging messages.

---

::: header
Next: [Other Misc Settings](Other-Misc-Settings.html#Other-Misc-Settings)]
:::
