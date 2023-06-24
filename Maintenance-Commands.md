---
tip: translate by openai@2023-06-24 00:00:51
...
---
description: Maintenance Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Maintenance Commands (Debugging with GDB)
lang: en
resource-type: document
title: Maintenance Commands (Debugging with GDB)
---
::: header
Next: [Remote Protocol](Remote-Protocol.html#Remote-Protocol)]
:::

---

## Appendix D Maintenance Commands


In addition to commands intended for [GDB] developers, that are not documented elsewhere in this manual. These commands are provided here for reference. (For commands that turn on debugging messages, see [Debugging Output](Debugging-Output.html#Debugging-Output).)

> 除了本手册中没有文档说明的针对GDB开发者的命令外，这里还提供了参考用的命令。（有关打开调试消息的命令，请参见[调试输出](Debugging-Output.html#Debugging-Output)。）

`maint agent [-at linespec,] expression`

`maint agent-eval [-at linespec,] expression`


Translate the given `expression` resolves (see [Linespec Locations](Linespec-Locations.html#Linespec-Locations)). If not, generate remote agent bytecode for current frame PC address.

> 解析给定表达式（参见[Linespec Locations]（Linespec-Locations.html#Linespec-Locations））。如果不能，则为当前帧PC地址生成远程代理字节码。

`maint agent-printf format,expr,...`


Translate the given format string and list of argument expressions into remote agent bytecodes and display them as a disassembled list. This command is useful for debugging the agent version of dynamic printf (see [Dynamic Printf](Dynamic-Printf.html#Dynamic-Printf)).

> 将给定的格式字符串和参数表达式转换成远程代理字节码，并将其作为反汇编列表显示出来。此命令有助于调试动态printf的代理版本（参见[Dynamic Printf](Dynamic-Printf.html#Dynamic-Printf））。

`maint info breakpoints`


Using the same format as '`info breakpoints` is using for internal purposes. Internal breakpoints are shown with negative breakpoint numbers. The type column identifies what kind of breakpoint is shown:

> 使用与'info breakpoints'相同的格式用于内部用途。内部断点以负断点号显示。类型列标识显示的是什么类型的断点：

`breakpoint`

:   Normal, explicitly set breakpoint.

`watchpoint`

:   Normal, explicitly set watchpoint.

`longjmp`


:   Internal breakpoint, used to handle correctly stepping through `longjmp` calls.

> 内部断点，用于正确处理“longjmp”调用的步进。

`longjmp resume`

:   Internal breakpoint at the target of a `longjmp`.

`until`

:   Temporary internal breakpoint used by the [GDB] `until` command.

`finish`

:   Temporary internal breakpoint used by the [GDB] `finish` command.

`shlib events`

:   Shared library events.

`maint info btrace`

Pint information about raw branch tracing data.

`maint btrace packet-history`


Print the raw branch trace packets that are used to compute the execution history for the '`record btrace`' command. Both the information and the format in which it is printed depend on the btrace recording format.

> 打印用于计算“record btrace”命令执行历史的原始分支跟踪数据包。信息和打印格式均取决于btrace记录格式。

`bts`


For the BTS recording format, print a list of blocks of sequential code. For each block, the following information is printed:

> 對於BTS錄製格式，列印一個代碼塊的列表。對於每個代碼塊，將打印以下信息：

Block number

Newer blocks have higher numbers. The oldest block has number zero.

Lowest '`PC`'

Highest '`PC`'

`pt`


For the Intel Processor Trace recording format, print a list of Intel Processor Trace packets. For each packet, the following information is printed:

> 对于Intel处理器跟踪记录格式，打印Intel处理器跟踪数据包的列表。对于每个数据包，打印以下信息：

Packet number

Newer packets have higher numbers. The oldest packet has number zero.

Trace offset

The packet's offset in the trace stream.

Packet opcode and payload

`maint btrace clear-packet-history`


Discards the cached packet history printed by the '`maint btrace packet-history`' command. The history will be computed again when needed.

> 清除由'maint btrace packet-history'命令打印的缓存的数据包历史记录。当需要时，历史记录将会重新计算。

`maint btrace clear`


Discard the branch trace data. The data will be fetched anew and the branch trace will be recomputed when needed.

> 丢弃分支跟踪数据。需要时将重新获取数据并重新计算分支跟踪。


This implicitly truncates the branch trace to a single branch trace buffer. When updating branch trace incrementally, the branch trace available to [GDB] may be bigger than a single branch trace buffer.

> 这隐式地将分支跟踪截断为单个分支跟踪缓冲区。当逐步更新分支跟踪时，可用于[GDB]的分支跟踪可能大于单个分支跟踪缓冲区。

`maint set btrace pt skip-pad`

`maint show btrace pt skip-pad`


Control whether [GDB] will skip PAD packets when computing the packet history.

> 控制GDB是否在计算数据包历史时跳过PAD数据包。

`maint info jit`

Print information about JIT code objects loaded in the current inferior.

`maint info python-disassemblers`


This command is defined within the `gdb.disassembler` Python module (see [Disassembly In Python](Disassembly-In-Python.html#Disassembly-In-Python)), and will only be present after that module has been imported. To force the module to be imported do the following:

> 这个命令定义在Python模块`gdb.disassembler`中（参见[Python中的反汇编](Disassembly-In-Python.html#Disassembly-In-Python)），只有在导入该模块后才会出现。要强制导入模块，请执行以下操作：

::: smallexample

```bash
(gdb) python import gdb.disassembler
```

:::


This command lists all the architectures for which a disassembler is currently registered, and the name of the disassembler. If a disassembler is registered for all architectures, then this is listed last against the '`GLOBAL`' architecture.

> 这个命令列出所有当前注册的反汇编器的体系结构，以及反汇编器的名称。如果为所有体系结构注册了反汇编器，那么最后会以'GLOBAL'体系结构列出。


If one of the disassemblers would be selected for the architecture of the current inferior, then this disassembler will be marked.

> 如果选择了一个反汇编器来处理当前下属的架构，那么这个反汇编器将被标记。


The following example shows a situation in which two disassemblers are registered, initially the '`i386`' disassembler matches.

> 以下示例展示了一种情况，其中注册了两个反汇编器，最初'i386'反汇编器匹配。

::: smallexample

```bash
(gdb) show architecture
The target architecture is set to "auto" (currently "i386").
(gdb) maint info python-disassemblers
Architecture        Disassember Name
i386                Disassembler_1  (Matches current architecture)
GLOBAL              Disassembler_2
```

```bash
(gdb) set architecture arm
The target architecture is set to "arm".
(gdb) maint info python-disassemblers
quit
Architecture        Disassember Name
i386                Disassembler_1
GLOBAL              Disassembler_2  (Matches current architecture)
```

:::

`set displaced-stepping`

`show displaced-stepping`


Control whether or not [GDB] will do *displaced stepping* if the target supports it. Displaced stepping is a way to single-step over breakpoints without removing them from the inferior, by executing an out-of-line copy of the instruction that was originally at the breakpoint location. It is also known as out-of-line single-stepping.

> 控制[GDB]是否会在目标支持时执行*替换步进*。替换步进是一种在不从下级中删除断点的情况下单步跳过断点的方法，通过执行原本位于断点位置的指令的外部副本。它也被称为外部单步。

`set displaced-stepping on`


:   If the target architecture supports it, [GDB] will use displaced stepping to step over breakpoints.

> 如果目标架构支持，[GDB]将使用移位步进来跳过断点。

`set displaced-stepping off`


:   [GDB] will not use displaced stepping to step over breakpoints, even if such is supported by the target architecture.

> GDB不会使用位移步进来跳过断点，即使这在目标架构中得到支持。

```

```

`set displaced-stepping auto`


:   This is the default mode. [GDB] will use displaced stepping only if non-stop mode is active (see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)) and the target architecture supports displaced stepping.

> 这是默认模式。如果非停止模式处于活动状态（参见[非停止模式](Non_002dStop-Mode.html#Non_002dStop-Mode))且目标架构支持位移步进，[GDB]将使用位移步进。

`maint check-psymtabs`


Check the consistency of currently expanded psymtabs versus symtabs. Use this to check, for example, whether a symbol is in one but not the other.

> 检查当前扩展的psymtabs与symtabs的一致性。可以用它来检查例如一个符号是否在一个中存在而在另一个中不存在。

`maint check-symtabs`

Check the consistency of currently expanded symtabs.

`maint expand-symtabs [regexp]`

Expand symbol tables. If `regexp`.

`maint set catch-demangler-crashes [on|off]`

`maint show catch-demangler-crashes`


Control whether [GDB] should attempt to catch crashes in the symbol name demangler. The default is to attempt to catch crashes. If enabled, the first time a crash is caught, a core file is created, the offending symbol is displayed and the user is presented with the option to terminate the current session.

> 控制GDB是否应尝试捕获符号名称解析器中的崩溃。默认是尝试捕获。如果启用，第一次捕获崩溃时，将创建一个核心文件，显示有害符号，并向用户提供终止当前会话的选项。

`maint cplus first_component name`

Print the first C++ class/namespace component of `name`.

`maint cplus namespace`

Print the list of possible C++ namespaces.

`maint deprecate command [replacement]`

`maint undeprecate command`


Deprecate or undeprecate the named `command` will mention the replacement as part of the warning.

> 将命名的`command`弃用或取消弃用，将会在警告中提及替代品。

`maint dump-me`


Cause a fatal signal in the debugger and force it to dump its core. This is supported only on systems which support aborting a program with the `SIGQUIT` signal.

> 因为调试器中的致命信号，并强制它转储其核心。这只支持那些支持使用`SIGQUIT`信号中止程序的系统。

`maint internal-error [message-text]`

`maint internal-warning [message-text]`

`maint demangler-warning [message-text]`

Cause [GDB] session.


These commands take an optional parameter `message-text` that is used as the text of the error or warning message.

> 这些命令接受一个可选参数`message-text`，用作错误或警告消息的文本。

Here's an example of using `internal-error`:

::: smallexample

```bash
(gdb) maint internal-error testing, 1, 2
…/maint.c:121: internal-error: testing, 1, 2
A problem internal to GDB has been detected.  Further
debugging may prove unreliable.
Quit this debugging session? (y or n) n
Create a core file? (y or n) n
(gdb)
```

:::

`maint set internal-error action [ask|yes|no]`

`maint show internal-error action`

`maint set internal-warning action [ask|yes|no]`

`maint show internal-warning action`

`maint set demangler-warning action [ask|yes|no]`

`maint show demangler-warning action`

When [GDB], described in the table below.

'`quit`'


:   You can specify that [GDB] should always (yes) or never (no) quit. The default is to ask the user what to do.

> 你可以指定GDB总是（是）或从不（否）退出。默认情况下询问用户该做什么。

'`corefile`'


:   You can specify that [GDB] should always (yes) or never (no) create a core file. The default is to ask the user what to do. Note that there is no `corefile` option for `demangler-warning`: demangler warnings always create a core file and this cannot be disabled.

> 你可以指定GDB总是（是）或永不（否）创建核心文件。默认情况下询问用户该做什么。请注意，demangler-warning没有`corefile`选项：demangler警告总是创建核心文件，且不能禁用。

`maint set internal-error backtrace [on|off]`

`maint show internal-error backtrace`

`maint set internal-warning backtrace [on|off]`

`maint show internal-warning backtrace`

When [GDB]' by default for `internal-warning`.

`maint packet text`

If [GDB]' character, and the checksum.


Any non-printable characters in the reply are printed as escaped hex, e.g. '`\x00`', etc.

> 回复中的任何非可打印字符将以转义十六进制形式打印，例如'\x00'等。

`maint print architecture [file]`


Print the entire architecture configuration. The optional argument `file` names the file where the output goes.

> 打印整个架构配置。可选参数`file`指定输出的文件名称。

`maint print c-tdesc [-single-feature] [file]`


Print the target description (see [Target Descriptions](Target-Descriptions.html#Target-Descriptions)) as a C source file. By default, the target description is for the current target, but if the optional argument `file` is built again. This command is used by developers after they add or modify XML target descriptions.

> 打印目标描述（参见[目标描述](Target-Descriptions.html#Target-Descriptions))作为C源文件。默认情况下，目标描述是为当前目标，但如果可选参数`file`被重新构建。此命令在开发人员添加或修改XML目标描述后使用。


When the optional flag '`-single-feature`) must only contain a single feature. The source file produced is different in this case.

> 在这种情况下，使用可选标志'-single-feature'时，源文件必须只包含一个特征。生成的源文件在这种情况下是不同的。

`maint print xml-tdesc  [file]`


Print the target description (see [Target Descriptions](Target-Descriptions.html#Target-Descriptions)) as an XML file. By default print the target description for the current target, but if the optional argument `file` should be an XML document, of the form described in [Target Description Format](Target-Description-Format.html#Target-Description-Format).

> 打印目标描述（参见[目标描述]（Target-Descriptions.html#Target-Descriptions））作为XML文件。默认情况下打印当前目标的目标描述，但如果可选参数`file`应该是一个XML文档，其格式如[目标描述格式]（Target-Description-Format.html#Target-Description-Format）所述。

`maint check xml-descriptions dir`

Check that the target descriptions dynamically created by [GDB].

`maint check libthread-db`


Run integrity checks on the current inferior's thread debugging library. This exercises all `libthread_db` functionality used by [GDB] that `libthread_db` uses. Note that parts of the test may be skipped on some platforms when debugging core files.

> 在当前线程调试库上运行完整性检查。这将检验[GDB]使用的所有`libthread_db`功能。请注意，在调试内核文件时，部分测试可能会被跳过。

`maint print core-file-backed-mappings`


Print the file-backed mappings which were loaded from a core file note. This output represents state internal to [GDB] and should be similar to the mappings displayed by the `info proc mappings` command.

> 打印从内核文件笔记中加载的文件映射。此输出表示[GDB]内部的状态，应与“info proc mappings”命令显示的映射相似。

`maint print dummy-frames`

Prints the contents of [GDB]'s internal dummy-frame stack.

::: smallexample

```bash
(gdb) b add
…
(gdb) print add(2,3)
Breakpoint 2, add (a=2, b=3) at …
58    return (a + b);
The program being debugged stopped while in a function called from GDB.
…
(gdb) maint print dummy-frames
0xa8206d8: id=, ptid=process 9353
(gdb)
```

:::

Takes an optional file parameter.

`maint print frame-id`

`maint print frame-id level`

Print [GDB] is not given.


If used, `level` should be an integer, as displayed in the `backtrace` output.

> 如果使用，“level”应该是一个整数，如“backtrace”输出中所示。

::: smallexample

```bash
(gdb) maint print frame-id
frame-id for frame #0: 
(gdb) maint print frame-id 2
frame-id for frame #2: 
```

:::

`maint print registers [file]`

`maint print raw-registers [file]`

`maint print cooked-registers [file]`

`maint print register-groups [file]`

`maint print remote-registers [file]`

Print [GDB]'s internal register data structures.


The command `maint print raw-registers` includes the contents of the raw register cache; the command `maint print cooked-registers` includes the (cooked) value of all registers, including registers which aren't available on the target nor visible to user; the command `maint print register-groups` includes the groups that each register is a member of; and the command `maint print remote-registers` includes the remote target's register numbers and offsets in the 'G' packets.

> 命令`maint print raw-registers`包括原始寄存器缓存的内容；命令`maint print cooked-registers`包括所有寄存器（经过处理的）的值，包括目标上不可用也不可见于用户的寄存器；命令`maint print register-groups`包括每个寄存器所属的组；而命令`maint print remote-registers`包括远程目标的寄存器编号和'G'数据包中的偏移量。


These commands take an optional parameter, a file name to which to write the information.

> 这些命令可以接受一个可选参数，即用于写入信息的文件名。

`maint print reggroups [file]`

Print [GDB] tells to what file to write the information.

The register groups info looks like this:

::: smallexample

```bash
(gdb) maint print reggroups
 Group      Type
 general    user
 float      user
 all        user
 vector     user
 system     user
 save       internal
 restore    internal
```

:::

`maint flush register-cache`

`flushregs`


Flush the contents of the register cache and as a consequence the frame cache. This command is useful when debugging issues related to register fetching, or frame unwinding. The command `flushregs` is deprecated in favor of `maint flush register-cache`.

> 清空寄存器缓存的内容，从而清空帧缓存。当调试与寄存器获取或帧展开相关的问题时，此命令非常有用。`flushregs`命令已被`maint flush register-cache`所取代。

`maint flush source-cache`


Flush [GDB] wants to show lines from a source file, the content will be re-read.

> GDB 想要显示来自源文件的行，内容将会重新读取。


This command is useful when debugging issues related to source code styling. After flushing the cache any source code displayed by [GDB] will be re-read and re-styled.

> 这个命令在调试与源代码样式有关的问题时很有用。在清空缓存后，[GDB]显示的任何源代码都将被重新读取和重新样式化。

`maint print objfiles [regexp]`


Print a dump of all known object files. If `regexp`. For each object file, this command prints its name, address in memory, and all of its psymtabs and symtabs.

> 打印所有已知对象文件的转储。如果`regexp`。对于每个对象文件，此命令会打印其名称、内存中的地址以及所有的psymtabs和symtabs。

`maint print user-registers`


List all currently available *user registers*. User registers typically provide alternate names for actual hardware registers. They include the four "standard" registers `$fp`, `$pc`, `$sp`, and `$ps`. See [standard registers](Registers.html#standard-registers). User registers can be used in expressions in the same way as the canonical register names, but only the latter are listed by the `info registers` and `maint print registers` commands.

> 列出当前可用的*用户寄存器*。用户寄存器通常为实际硬件寄存器提供替代名称。它们包括四个“标准”寄存器`$fp`、`$pc`、`$sp`和`$ps`。请参阅[标准寄存器](Registers.html#standard-registers)。用户寄存器可以像规范寄存器名称一样在表达式中使用，但只有后者会被`info registers`和`maint print registers`命令列出。

`maint print section-scripts [regexp]`


Print a dump of scripts specified in the `.debug_gdb_section` section. If `regexp`. For each script, this command prints its name as specified in the objfile, and the full path if known. See [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section).

> 打印`.debug_gdb_section`部分指定的脚本的转储。如果有`regexp`。对于每个脚本，此命令会打印其在objfile中指定的名称，以及已知的完整路径。请参见[dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)。

`maint print statistics`


This command prints, for each object file in the program, various data about that object file followed by the byte cache (*bcache*) statistics for the object file. The objfile data includes the number of minimal, partial, full, and stabs symbols, the number of types defined by the objfile, the number of as yet unexpanded psym tables, the number of line tables and string tables, and the amount of memory used by the various tables. The bcache statistics include the counts, sizes, and counts of duplicates of all and unique objects, max, average, and median entry size, total memory used and its overhead and savings, and various measures of the hash table size and chain lengths.

> 这个命令会打印程序中每个对象文件的各种数据，后跟字节缓存（*bcache*）统计信息。对象文件数据包括最小、部分、完整和stabs符号的数量，对象文件定义的类型数量，尚未展开的psym表的数量，行表和字符串表的数量以及各种表所使用的内存量。bcache统计信息包括所有和唯一对象的计数、大小和重复计数，最大、平均和中值条目大小，总内存使用量及其开销和节省，以及哈希表大小和链长的各种度量。

`maint print target-stack`


A *target* is an interface between the debugger and a particular kind of file or process. Targets can be stacked in *strata*, so that more than one target can potentially respond to a request. In particular, memory accesses will walk down the stack of targets until they find a target that is interested in handling that particular address.

> 一个*目标*是调试器和特定类型文件或进程之间的接口。目标可以分层次堆叠，因此可以有多个目标可能响应请求。特别是，内存访问将沿着目标堆栈向下走，直到找到感兴趣处理该特定地址的目标。


This command prints a short description of each layer that was pushed on the *target stack*, starting from the top layer down to the bottom one.

> 这个命令打印出每一层推送到*目标堆栈*上的简短描述，从顶层到底层。

`maint print type expr`


Print the type chain for a type specified by `expr`'s data structures, including its flags and contained types.

> 打印由`expr`的数据结构指定的类型的类型链，包括其标志和包含的类型。

`maint print record-instruction`

`maint print record-instruction N`


print how GDB recorded a given instruction. If `n` is not given, 0 is assumed.

> 打印GDB如何记录给定指令。如果没有给定n，则假定为0。

`maint selftest [-verbose] [filter]`


Run any self tests that were compiled in to [GDB] in their name will be ran. If `-verbose` is passed, the self tests can be more verbose.

> 运行编译到GDB中的任何自检测，它们的名称将被运行。如果传入`-verbose`，自检测可以更详细。

`maint set selftest verbose`

`maint show selftest verbose`

Control whether self tests are run verbosely or not.

`maint info selftests`

List the selftests compiled in to [GDB].

`maint set dwarf always-disassemble`

`maint show dwarf always-disassemble`


Control the behavior of `info address` when using DWARF debugging information.

> 控制使用DWARF调试信息时`info address`的行为。


The default is `off`, which means that [GDB] to describe simply; in this case you will always see the disassembly form.

> 默认是关闭的，这意味着[GDB]简单描述；在这种情况下，你将总是看到反汇编形式。

Here is an example of the resulting disassembly:

::: smallexample

```bash
(gdb) info addr argc
Symbol "argc" is a complex DWARF expression:
     1: DW_OP_fbreg 0
```

:::


For more information on these expressions, see [the DWARF standard](http://www.dwarfstd.org/).

> 欲了解更多关于这些表达式的信息，请参阅[DWARF标准](http://www.dwarfstd.org/)。

`maint set dwarf max-cache-age`

`maint show dwarf max-cache-age`

Control the DWARF compilation unit cache.


In object files with inter-compilation-unit references, such as those produced by the GCC option '`-feliminate-dwarf2-dups` startup, but reduce memory consumption.

> 在使用GCC选项“-feliminate-dwarf2-dups”生成的具有跨编译单元引用的对象文件中，可以减少启动时间，但降低内存消耗。

`maint set dwarf unwinders`

`maint show dwarf unwinders`

Control use of the DWARF frame unwinders.


Many targets that support DWARF debugging use [GDB]'s DWARF frame unwinders to build the backtrace. Many of these targets will also have a second mechanism for building the backtrace for use in cases where DWARF information is not available, this second mechanism is often an analysis of a function's prologue.

> 许多支持DWARF调试的目标都使用GDB的DWARF框架解开器来构建回溯。其中许多目标在没有DWARF信息的情况下也会有第二种机制来构建回溯，这种第二种机制通常是对函数序言的分析。


In order to extend testing coverage of the second level stack unwinding mechanisms it is helpful to be able to disable the DWARF stack unwinders, this can be done with this switch.

> 为了扩展第二级堆栈展开机制的测试覆盖范围，有助于能够禁用DWARF堆栈展开器，可以使用此开关来实现。


In normal use of [GDB] disabling the DWARF unwinders is not advisable, there are cases that are better handled through DWARF than prologue analysis, and the debug experience is likely to be better with the DWARF frame unwinders enabled.

> 在正常使用GDB时，不建议禁用DWARF解开器，有些情况可以通过DWARF比通过序言分析更好地处理，启用DWARF帧解开器可能会得到更好的调试体验。


If DWARF frame unwinders are not supported for a particular target architecture, then enabling this flag does not cause them to be used.

> 如果特定目标架构不支持矮人框架卸载器，那么启用此标志不会导致它们被使用。

`maint info frame-unwinders`


List the frame unwinders currently in effect, starting with the highest priority.

> 列出当前生效的框架解卷器，优先级从高到低。

`maint set worker-threads`

`maint show worker-threads`


Control the number of worker threads that may be used by [GDB] may start threads of their own.

> 控制[GDB]可以使用的工作线程数量，它们可以启动自己的线程。

`maint set profile`

`maint show profile`

Control profiling of [GDB].


Profiling will be disabled until you use the '`maint set profile` file, be sure to move it to a safe location.

> 调试将被禁用，直到您使用“maint set profile”文件，请务必将其移至安全位置。

Configuring with '`--enable-profiling`' compiler option.

`maint set show-debug-regs`

`maint show show-debug-regs`


Control whether to show variables that mirror the hardware debug registers. Use `on` to enable, `off` to disable. If enabled, the debug registers values are shown when [GDB] inserts or removes a hardware breakpoint or watchpoint, and when the inferior triggers a hardware-assisted breakpoint or watchpoint.

> 控制是否显示镜像硬件调试寄存器的变量。使用 `on` 来启用，使用 `off` 来禁用。如果启用，当 [GDB] 插入或移除硬件断点或监视点，以及当下属触发硬件辅助断点或监视点时，会显示调试寄存器的值。

`maint set show-all-tib`

`maint show show-all-tib`


Control whether to show all non zero areas within a 1k block starting at thread local base, when using the '`info w32 thread-information-block`' command.

> 控制在使用“info w32 thread-information-block”命令时，是否显示从线程本地基础开始的1k块内的所有非零区域。

`maint set target-async`

`maint show target-async`


This controls whether [GDB] targets operate in synchronous or asynchronous mode (see [Background Execution](Background-Execution.html#Background-Execution)). Normally the default is asynchronous, if it is available; but this can be changed to more easily debug problems occurring only in synchronous mode.

> 这控制[GDB]目标是否以同步或异步模式运行（参见[后台执行](Background-Execution.html#Background-Execution)）。通常默认情况下是异步，如果可用；但可以更改以更容易调试只在同步模式下出现的问题。

`maint set target-non-stop`

`maint show target-non-stop`


This controls whether [GDB] targets always operate in non-stop mode even if `set non-stop` is `off` (see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)). The default is `auto`, meaning non-stop mode is enabled if supported by the target.

> 这控制[GDB]目标是否总是以非停止模式运行，即使`set non-stop`设置为`off`（请参见[非停止模式](Non_002dStop-Mode.html#Non_002dStop-Mode)）。默认值为`auto`，意味着如果目标支持，则启用非停止模式。

`maint set target-non-stop auto`


:   This is the default mode. [GDB] controls the target in non-stop mode if the target supports it.

> 这是默认模式。如果目标支持，GDB将以非停止模式控制目标。

`maint set target-non-stop on`


:   [GDB] controls the target in non-stop mode even if the target does not indicate support.

> GDB 可以在目标不支持的情况下以非停止模式控制目标。

`maint set target-non-stop off`


:   [GDB] does not control the target in non-stop mode even if the target supports it.

> GDB在非停止模式下即使目标支持它也不能控制目标。

`maint set tui-resize-message`

`maint show tui-resize-message`


Control whether [GDB] will display a message after a resize is completed; the message will include a number indicating how many times the terminal has been resized. This setting is intended for use by the test suite, where it would otherwise be difficult to determine when a resize and refresh has been completed.

> 控制[GDB]在调整大小完成后是否显示消息；该消息将包括一个数字，指示终端已经调整大小的次数。此设置旨在供测试套件使用，否则很难确定调整大小和刷新何时完成。

`maint set tui-left-margin-verbose`

`maint show tui-left-margin-verbose`


Control whether the left margin of the TUI source and disassembly windows uses '`_`' at locations where otherwise there would be a space. The default is `off`, which means spaces are used. The setting is intended to make it clear where the left margin begins and ends, to avoid incorrectly interpreting a space as being part of the the left margin.

> 控制源代码和反汇编窗口的左边距是否使用“_”来代替空格。默认是关闭的，这意味着使用空格。此设置旨在清楚地表明左边距的开始和结束位置，以避免错误地将空格解释为左边距的一部分。

`maint set per-command`

`maint show per-command`


[GDB] can display the resources used by each command. This is useful in debugging performance problems.

> [GDB]可以显示每个命令使用的资源。这在调试性能问题时很有用。

`maint set per-command space [on|off]`
`maint show per-command space`


:   Enable or disable the printing of the memory used by GDB for each command. If enabled, [GDB] command-line switch (see [Mode Options](Mode-Options.html#Mode-Options)).

> 启用或禁用打印GDB用于每个命令的内存。如果启用，[GDB]命令行开关（参见[模式选项](Mode-Options.html#Mode-Options))。

`maint set per-command time [on|off]`
`maint show per-command time`


:   Enable or disable the printing of the execution time of [GDB] command-line switch (see [Mode Options](Mode-Options.html#Mode-Options)).

> 启用或禁用[GDB]命令行开关的执行时间的打印（参见[Mode Options](Mode-Options.html#Mode-Options)）。

`maint set per-command symtab [on|off]`
`maint show per-command symtab`


:   Enable or disable the printing of basic symbol table statistics for each command. If enabled, [GDB] will display the following information:

> 启用或禁用为每个命令打印基本符号表统计信息。如果启用，[GDB]将显示以下信息：

```
a.  number of symbol tables
b.  number of primary symbol tables
c.  number of blocks in the blockvector
```

`maint set check-libthread-db [on|off]`

`maint show check-libthread-db`


Control whether [GDB] will unload the library and continue searching for a suitable candidate as described in [set libthread-db-search-path](Threads.html#set-libthread_002ddb_002dsearch_002dpath). For more information about the tests, see [maint check libthread-db](#maint-check-libthread_002ddb).

> 控制GDB是否卸载库并根据[设置libthread-db-search-path](Threads.html#set-libthread_002ddb_002dsearch_002dpath)中的说明继续搜索合适的候选项。有关测试的更多信息，请参阅[maint check libthread-db](#maint-check-libthread_002ddb)。

`maint set gnu-source-highlight enabled [on|off]`

`maint show gnu-source-highlight enabled`

Control whether [GDB]' will give an error.


If the GNU Source Highlight library is not being used, then [GDB] will use the Python Pygments package for source code styling, if it is available.

> 如果没有使用GNU源代码高亮库，那么[GDB]将会使用可用的Python Pygments包来格式化源代码。


This option is useful for debugging [GDB] is linked against the GNU Source Highlight library.

> 这个选项对于调试有用，因为GDB与GNU源代码高亮库相关联。

`maint set libopcodes-styling enabled [on|off]`

`maint show libopcodes-styling enabled`


Control whether [GDB]) to style disassembler output (see [Output Styling](Output-Styling.html#Output-Styling)). The builtin disassembler does not support styling for all architectures.

> 控制GDB是否对反汇编输出进行样式控制（参见[输出样式](Output-Styling.html#Output-Styling))。内置的反汇编器不支持所有架构的样式控制。


When this option is '`off` will fall back to using the Python Pygments package if possible.

> 当此选项设置为“关闭”时，将尝试使用Python Pygments包。


Trying to set this option '`on`' for an architecture that the builtin disassembler is unable to style will give an error, otherwise, the builtin disassembler will be used to style disassembler output.

> 尝试为无法使用内置反汇编器样式的架构设置此选项'on'将会出错，否则将使用内置反汇编器来样式反汇编器输出。

This option is '`on`' by default for supported architectures.


This option is useful for debugging [GDB] is built for an architecture that supports styling with the builtin disassembler

> 这个选项对于调试GDB很有用，因为它针对支持内置反汇编器的架构进行构建。

`maint info screen`


Print various characteristics of the screen, such as various notions of width and height.

> 打印屏幕的各种特性，如宽度和高度的各种概念。

`maint space value`


An alias for `maint set per-command space`. A non-zero value enables it, zero disables it.

> 一个别名 `maint set per-command space`。 非零值启用它，零禁用它。

`maint time value`


An alias for `maint set per-command time`. A non-zero value enables it, zero disables it.

> 一个别名，用于`maint set per-command time`。非零值启用它，零禁用它。

`maint translate-address [section] addr`


Find the symbol stored at the location specified by the address `addr` prints the name of the closest symbol and an offset from the symbol's location to the specified address. This is similar to the `info address` command (see [Symbols](Symbols.html#Symbols)), except that this command also allows to find symbols in other sections.

> 在地址`addr`指定的位置找到符号，输出最接近的符号的名称以及该符号位置到指定地址的偏移量。这与`info address`命令类似（参见[符号](Symbols.html#Symbols)），但此命令还允许在其他部分中查找符号。


If section was not specified, the section in which the symbol was found is also printed. For dynamically linked executables, the name of executable or shared library containing the symbol is printed as well.

> 如果没有指定段，也会打印出找到符号的段。对于动态链接的可执行文件，也会打印出包含该符号的可执行文件或共享库的名称。

`maint test-options require-delimiter`

`maint test-options unknown-is-error`

`maint test-options unknown-is-operand`


These commands are used by the testsuite to validate the command options framework. The `require-delimiter` variant requires a double-dash delimiter to indicate end of options. The `unknown-is-error` and `unknown-is-operand` do not. The `unknown-is-error` variant throws an error on unknown option, while `unknown-is-operand` treats unknown options as the start of the command's operands. When run, the commands output the result of the processed options. When completed, the commands store the internal result of completion in a variable exposed by the `maint show test-options-completion-result` command.

> 这些命令被测试套件用来验证命令选项框架。`require-delimiter`变体需要双破折号分隔符来指示选项结束。`unknown-is-error`和`unknown-is-operand`不需要。`unknown-is-error`变体在未知选项上抛出错误，而`unknown-is-operand`将未知选项视为命令操作数的开始。运行时，命令会输出处理选项的结果。完成时，命令会将完成的内部结果存储在`maint show test-options-completion-result`命令暴露的变量中。

`maint show test-options-completion-result`


Shows the result of completing the `maint test-options` subcommands. This is used by the testsuite to validate completion support in the command options framework.

> 显示完成`maint test-options`子命令的结果。这被测试套件用来验证命令选项框架中的完成支持。

`maint set test-settings kind`

`maint show test-settings kind`


These are representative commands for each `kind` supports. They are used by the testsuite for exercising the settings infrastructure.

> 这些是每种`类型`支持的代表性命令。它们被测试套件用来锻炼设置基础设施。

`maint set backtrace-on-fatal-signal [on|off]`

`maint show backtrace-on-fatal-signal`

When this setting is `on`, if [GDB] developers.


If the functionality to provide this backtrace is not available for the platform on which GDB is running then this feature will be `off` by default, and attempting to turn this feature on will give an error.

> 如果GDB运行的平台上没有提供此回溯功能，则此功能将默认关闭，尝试打开此功能将会出错。


For platforms that do support creating the backtrace this feature is `on` by default.

> 对于支持创建回溯的平台，此功能默认为`开`状态。

`maint wait-for-index-cache`


Wait until all pending writes to the index cache have completed. This is used by the test suite to avoid races when the index cache is being updated by a worker thread.

> 等待所有对索引缓存的写入完成。这用于测试套件，以避免当工作线程正在更新索引缓存时出现竞争。

`maint with setting [value] [-- command]`


Like the `with` command, but works with `maintenance set` variables. This is used by the testsuite to exercise the `with` command's infrastructure.

> 就像`with`命令一样，但是使用`maintenance set`变量。 这被测试套件用来练习`with`命令的基础设施。

`maint ignore-probes [-v|-verbose] [provider [name [objfile]]]`

`maint ignore-probes -reset`


Set or reset the ignore-probes filter. The `provider` arguments are as in `enable probes` and `disable probes` (see [enable probes](Static-Probe-Points.html#enable-probes)). Only supported for SystemTap probes.

> 设置或重置忽略探测过滤器。`provider`参数与`enable probes`和`disable probes`（请参见[enable probes]（Static-Probe-Points.html#enable-probes））中的参数相同。仅支持SystemTap探测。

Here's an example of using `maint ignore-probes`:

::: smallexample

```bash
(gdb) maint ignore-probes -verbose libc ^longjmp$
ignore-probes filter has been set to:
PROVIDER: 'libc'
PROBE_NAME: '^longjmp$'
OBJNAME: ''
(gdb) start
<... more output ...>
Ignoring SystemTap probe libc longjmp in /lib64/libc.so.6.^M
Ignoring SystemTap probe libc longjmp in /lib64/libc.so.6.^M
Ignoring SystemTap probe libc longjmp in /lib64/libc.so.6.^M
```

:::


The following command is useful for non-interactive invocations of [GDB], such as in the test suite.

> 以下命令对于[GDB]的非交互式调用（如测试套件）很有用。

`set watchdog nsec`

:

```
Set the maximum number of seconds [GDB] reports and error and the command is aborted.
```

`show watchdog`

:   Show the current setting of the target wait timeout.

---

::: header
Next: [Remote Protocol](Remote-Protocol.html#Remote-Protocol)]
:::
