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

`maint agent [-at linespec,] expression`

`maint agent-eval [-at linespec,] expression`

Translate the given `expression` resolves (see [Linespec Locations](Linespec-Locations.html#Linespec-Locations)). If not, generate remote agent bytecode for current frame PC address.

`maint agent-printf format,expr,...`

Translate the given format string and list of argument expressions into remote agent bytecodes and display them as a disassembled list. This command is useful for debugging the agent version of dynamic printf (see [Dynamic Printf](Dynamic-Printf.html#Dynamic-Printf)).

`maint info breakpoints`

Using the same format as '`info breakpoints` is using for internal purposes. Internal breakpoints are shown with negative breakpoint numbers. The type column identifies what kind of breakpoint is shown:

`breakpoint`

:   Normal, explicitly set breakpoint.

`watchpoint`

:   Normal, explicitly set watchpoint.

`longjmp`

:   Internal breakpoint, used to handle correctly stepping through `longjmp` calls.

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

`bts`

For the BTS recording format, print a list of blocks of sequential code. For each block, the following information is printed:

Block number

Newer blocks have higher numbers. The oldest block has number zero.

Lowest '`PC`'

Highest '`PC`'

`pt`

For the Intel Processor Trace recording format, print a list of Intel Processor Trace packets. For each packet, the following information is printed:

Packet number

Newer packets have higher numbers. The oldest packet has number zero.

Trace offset

The packet's offset in the trace stream.

Packet opcode and payload

`maint btrace clear-packet-history`

Discards the cached packet history printed by the '`maint btrace packet-history`' command. The history will be computed again when needed.

`maint btrace clear`

Discard the branch trace data. The data will be fetched anew and the branch trace will be recomputed when needed.

This implicitly truncates the branch trace to a single branch trace buffer. When updating branch trace incrementally, the branch trace available to [GDB] may be bigger than a single branch trace buffer.

`maint set btrace pt skip-pad`

`maint show btrace pt skip-pad`

Control whether [GDB] will skip PAD packets when computing the packet history.

`maint info jit`

Print information about JIT code objects loaded in the current inferior.

`maint info python-disassemblers`

This command is defined within the `gdb.disassembler` Python module (see [Disassembly In Python](Disassembly-In-Python.html#Disassembly-In-Python)), and will only be present after that module has been imported. To force the module to be imported do the following:

::: smallexample

```bash
(gdb) python import gdb.disassembler
```

:::

This command lists all the architectures for which a disassembler is currently registered, and the name of the disassembler. If a disassembler is registered for all architectures, then this is listed last against the '`GLOBAL`' architecture.

If one of the disassemblers would be selected for the architecture of the current inferior, then this disassembler will be marked.

The following example shows a situation in which two disassemblers are registered, initially the '`i386`' disassembler matches.

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

`set displaced-stepping on`

:   If the target architecture supports it, [GDB] will use displaced stepping to step over breakpoints.

`set displaced-stepping off`

:   [GDB] will not use displaced stepping to step over breakpoints, even if such is supported by the target architecture.

```

```

`set displaced-stepping auto`

:   This is the default mode. [GDB] will use displaced stepping only if non-stop mode is active (see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)) and the target architecture supports displaced stepping.

`maint check-psymtabs`

Check the consistency of currently expanded psymtabs versus symtabs. Use this to check, for example, whether a symbol is in one but not the other.

`maint check-symtabs`

Check the consistency of currently expanded symtabs.

`maint expand-symtabs [regexp]`

Expand symbol tables. If `regexp`.

`maint set catch-demangler-crashes [on|off]`

`maint show catch-demangler-crashes`

Control whether [GDB] should attempt to catch crashes in the symbol name demangler. The default is to attempt to catch crashes. If enabled, the first time a crash is caught, a core file is created, the offending symbol is displayed and the user is presented with the option to terminate the current session.

`maint cplus first_component name`

Print the first C++ class/namespace component of `name`.

`maint cplus namespace`

Print the list of possible C++ namespaces.

`maint deprecate command [replacement]`

`maint undeprecate command`

Deprecate or undeprecate the named `command` will mention the replacement as part of the warning.

`maint dump-me`

Cause a fatal signal in the debugger and force it to dump its core. This is supported only on systems which support aborting a program with the `SIGQUIT` signal.

`maint internal-error [message-text]`

`maint internal-warning [message-text]`

`maint demangler-warning [message-text]`

Cause [GDB] session.

These commands take an optional parameter `message-text` that is used as the text of the error or warning message.

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

'`corefile`'

:   You can specify that [GDB] should always (yes) or never (no) create a core file. The default is to ask the user what to do. Note that there is no `corefile` option for `demangler-warning`: demangler warnings always create a core file and this cannot be disabled.

`maint set internal-error backtrace [on|off]`

`maint show internal-error backtrace`

`maint set internal-warning backtrace [on|off]`

`maint show internal-warning backtrace`

When [GDB]' by default for `internal-warning`.

`maint packet text`

If [GDB]' character, and the checksum.

Any non-printable characters in the reply are printed as escaped hex, e.g. '`\x00`', etc.

`maint print architecture [file]`

Print the entire architecture configuration. The optional argument `file` names the file where the output goes.

`maint print c-tdesc [-single-feature] [file]`

Print the target description (see [Target Descriptions](Target-Descriptions.html#Target-Descriptions)) as a C source file. By default, the target description is for the current target, but if the optional argument `file` is built again. This command is used by developers after they add or modify XML target descriptions.

When the optional flag '`-single-feature`) must only contain a single feature. The source file produced is different in this case.

`maint print xml-tdesc  [file]`

Print the target description (see [Target Descriptions](Target-Descriptions.html#Target-Descriptions)) as an XML file. By default print the target description for the current target, but if the optional argument `file` should be an XML document, of the form described in [Target Description Format](Target-Description-Format.html#Target-Description-Format).

`maint check xml-descriptions dir`

Check that the target descriptions dynamically created by [GDB].

`maint check libthread-db`

Run integrity checks on the current inferior's thread debugging library. This exercises all `libthread_db` functionality used by [GDB] that `libthread_db` uses. Note that parts of the test may be skipped on some platforms when debugging core files.

`maint print core-file-backed-mappings`

Print the file-backed mappings which were loaded from a core file note. This output represents state internal to [GDB] and should be similar to the mappings displayed by the `info proc mappings` command.

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

These commands take an optional parameter, a file name to which to write the information.

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

`maint flush source-cache`

Flush [GDB] wants to show lines from a source file, the content will be re-read.

This command is useful when debugging issues related to source code styling. After flushing the cache any source code displayed by [GDB] will be re-read and re-styled.

`maint print objfiles [regexp]`

Print a dump of all known object files. If `regexp`. For each object file, this command prints its name, address in memory, and all of its psymtabs and symtabs.

`maint print user-registers`

List all currently available *user registers*. User registers typically provide alternate names for actual hardware registers. They include the four "standard" registers `$fp`, `$pc`, `$sp`, and `$ps`. See [standard registers](Registers.html#standard-registers). User registers can be used in expressions in the same way as the canonical register names, but only the latter are listed by the `info registers` and `maint print registers` commands.

`maint print section-scripts [regexp]`

Print a dump of scripts specified in the `.debug_gdb_section` section. If `regexp`. For each script, this command prints its name as specified in the objfile, and the full path if known. See [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section).

`maint print statistics`

This command prints, for each object file in the program, various data about that object file followed by the byte cache (*bcache*) statistics for the object file. The objfile data includes the number of minimal, partial, full, and stabs symbols, the number of types defined by the objfile, the number of as yet unexpanded psym tables, the number of line tables and string tables, and the amount of memory used by the various tables. The bcache statistics include the counts, sizes, and counts of duplicates of all and unique objects, max, average, and median entry size, total memory used and its overhead and savings, and various measures of the hash table size and chain lengths.

`maint print target-stack`

A *target* is an interface between the debugger and a particular kind of file or process. Targets can be stacked in *strata*, so that more than one target can potentially respond to a request. In particular, memory accesses will walk down the stack of targets until they find a target that is interested in handling that particular address.

This command prints a short description of each layer that was pushed on the *target stack*, starting from the top layer down to the bottom one.

`maint print type expr`

Print the type chain for a type specified by `expr`'s data structures, including its flags and contained types.

`maint print record-instruction`

`maint print record-instruction N`

print how GDB recorded a given instruction. If `n` is not given, 0 is assumed.

`maint selftest [-verbose] [filter]`

Run any self tests that were compiled in to [GDB] in their name will be ran. If `-verbose` is passed, the self tests can be more verbose.

`maint set selftest verbose`

`maint show selftest verbose`

Control whether self tests are run verbosely or not.

`maint info selftests`

List the selftests compiled in to [GDB].

`maint set dwarf always-disassemble`

`maint show dwarf always-disassemble`

Control the behavior of `info address` when using DWARF debugging information.

The default is `off`, which means that [GDB] to describe simply; in this case you will always see the disassembly form.

Here is an example of the resulting disassembly:

::: smallexample

```bash
(gdb) info addr argc
Symbol "argc" is a complex DWARF expression:
     1: DW_OP_fbreg 0
```

:::

For more information on these expressions, see [the DWARF standard](http://www.dwarfstd.org/).

`maint set dwarf max-cache-age`

`maint show dwarf max-cache-age`

Control the DWARF compilation unit cache.

In object files with inter-compilation-unit references, such as those produced by the GCC option '`-feliminate-dwarf2-dups` startup, but reduce memory consumption.

`maint set dwarf unwinders`

`maint show dwarf unwinders`

Control use of the DWARF frame unwinders.

Many targets that support DWARF debugging use [GDB]'s DWARF frame unwinders to build the backtrace. Many of these targets will also have a second mechanism for building the backtrace for use in cases where DWARF information is not available, this second mechanism is often an analysis of a function's prologue.

In order to extend testing coverage of the second level stack unwinding mechanisms it is helpful to be able to disable the DWARF stack unwinders, this can be done with this switch.

In normal use of [GDB] disabling the DWARF unwinders is not advisable, there are cases that are better handled through DWARF than prologue analysis, and the debug experience is likely to be better with the DWARF frame unwinders enabled.

If DWARF frame unwinders are not supported for a particular target architecture, then enabling this flag does not cause them to be used.

`maint info frame-unwinders`

List the frame unwinders currently in effect, starting with the highest priority.

`maint set worker-threads`

`maint show worker-threads`

Control the number of worker threads that may be used by [GDB] may start threads of their own.

`maint set profile`

`maint show profile`

Control profiling of [GDB].

Profiling will be disabled until you use the '`maint set profile` file, be sure to move it to a safe location.

Configuring with '`--enable-profiling`' compiler option.

`maint set show-debug-regs`

`maint show show-debug-regs`

Control whether to show variables that mirror the hardware debug registers. Use `on` to enable, `off` to disable. If enabled, the debug registers values are shown when [GDB] inserts or removes a hardware breakpoint or watchpoint, and when the inferior triggers a hardware-assisted breakpoint or watchpoint.

`maint set show-all-tib`

`maint show show-all-tib`

Control whether to show all non zero areas within a 1k block starting at thread local base, when using the '`info w32 thread-information-block`' command.

`maint set target-async`

`maint show target-async`

This controls whether [GDB] targets operate in synchronous or asynchronous mode (see [Background Execution](Background-Execution.html#Background-Execution)). Normally the default is asynchronous, if it is available; but this can be changed to more easily debug problems occurring only in synchronous mode.

`maint set target-non-stop`

`maint show target-non-stop`

This controls whether [GDB] targets always operate in non-stop mode even if `set non-stop` is `off` (see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)). The default is `auto`, meaning non-stop mode is enabled if supported by the target.

`maint set target-non-stop auto`

:   This is the default mode. [GDB] controls the target in non-stop mode if the target supports it.

`maint set target-non-stop on`

:   [GDB] controls the target in non-stop mode even if the target does not indicate support.

`maint set target-non-stop off`

:   [GDB] does not control the target in non-stop mode even if the target supports it.

`maint set tui-resize-message`

`maint show tui-resize-message`

Control whether [GDB] will display a message after a resize is completed; the message will include a number indicating how many times the terminal has been resized. This setting is intended for use by the test suite, where it would otherwise be difficult to determine when a resize and refresh has been completed.

`maint set tui-left-margin-verbose`

`maint show tui-left-margin-verbose`

Control whether the left margin of the TUI source and disassembly windows uses '`_`' at locations where otherwise there would be a space. The default is `off`, which means spaces are used. The setting is intended to make it clear where the left margin begins and ends, to avoid incorrectly interpreting a space as being part of the the left margin.

`maint set per-command`

`maint show per-command`

[GDB] can display the resources used by each command. This is useful in debugging performance problems.

`maint set per-command space [on|off]`
`maint show per-command space`

:   Enable or disable the printing of the memory used by GDB for each command. If enabled, [GDB] command-line switch (see [Mode Options](Mode-Options.html#Mode-Options)).

`maint set per-command time [on|off]`
`maint show per-command time`

:   Enable or disable the printing of the execution time of [GDB] command-line switch (see [Mode Options](Mode-Options.html#Mode-Options)).

`maint set per-command symtab [on|off]`
`maint show per-command symtab`

:   Enable or disable the printing of basic symbol table statistics for each command. If enabled, [GDB] will display the following information:

```
a.  number of symbol tables
b.  number of primary symbol tables
c.  number of blocks in the blockvector
```

`maint set check-libthread-db [on|off]`

`maint show check-libthread-db`

Control whether [GDB] will unload the library and continue searching for a suitable candidate as described in [set libthread-db-search-path](Threads.html#set-libthread_002ddb_002dsearch_002dpath). For more information about the tests, see [maint check libthread-db](#maint-check-libthread_002ddb).

`maint set gnu-source-highlight enabled [on|off]`

`maint show gnu-source-highlight enabled`

Control whether [GDB]' will give an error.

If the GNU Source Highlight library is not being used, then [GDB] will use the Python Pygments package for source code styling, if it is available.

This option is useful for debugging [GDB] is linked against the GNU Source Highlight library.

`maint set libopcodes-styling enabled [on|off]`

`maint show libopcodes-styling enabled`

Control whether [GDB]) to style disassembler output (see [Output Styling](Output-Styling.html#Output-Styling)). The builtin disassembler does not support styling for all architectures.

When this option is '`off` will fall back to using the Python Pygments package if possible.

Trying to set this option '`on`' for an architecture that the builtin disassembler is unable to style will give an error, otherwise, the builtin disassembler will be used to style disassembler output.

This option is '`on`' by default for supported architectures.

This option is useful for debugging [GDB] is built for an architecture that supports styling with the builtin disassembler

`maint info screen`

Print various characteristics of the screen, such as various notions of width and height.

`maint space value`

An alias for `maint set per-command space`. A non-zero value enables it, zero disables it.

`maint time value`

An alias for `maint set per-command time`. A non-zero value enables it, zero disables it.

`maint translate-address [section] addr`

Find the symbol stored at the location specified by the address `addr` prints the name of the closest symbol and an offset from the symbol's location to the specified address. This is similar to the `info address` command (see [Symbols](Symbols.html#Symbols)), except that this command also allows to find symbols in other sections.

If section was not specified, the section in which the symbol was found is also printed. For dynamically linked executables, the name of executable or shared library containing the symbol is printed as well.

`maint test-options require-delimiter`

`maint test-options unknown-is-error`

`maint test-options unknown-is-operand`

These commands are used by the testsuite to validate the command options framework. The `require-delimiter` variant requires a double-dash delimiter to indicate end of options. The `unknown-is-error` and `unknown-is-operand` do not. The `unknown-is-error` variant throws an error on unknown option, while `unknown-is-operand` treats unknown options as the start of the command's operands. When run, the commands output the result of the processed options. When completed, the commands store the internal result of completion in a variable exposed by the `maint show test-options-completion-result` command.

`maint show test-options-completion-result`

Shows the result of completing the `maint test-options` subcommands. This is used by the testsuite to validate completion support in the command options framework.

`maint set test-settings kind`

`maint show test-settings kind`

These are representative commands for each `kind` supports. They are used by the testsuite for exercising the settings infrastructure.

`maint set backtrace-on-fatal-signal [on|off]`

`maint show backtrace-on-fatal-signal`

When this setting is `on`, if [GDB] developers.

If the functionality to provide this backtrace is not available for the platform on which GDB is running then this feature will be `off` by default, and attempting to turn this feature on will give an error.

For platforms that do support creating the backtrace this feature is `on` by default.

`maint wait-for-index-cache`

Wait until all pending writes to the index cache have completed. This is used by the test suite to avoid races when the index cache is being updated by a worker thread.

`maint with setting [value] [-- command]`

Like the `with` command, but works with `maintenance set` variables. This is used by the testsuite to exercise the `with` command's infrastructure.

`maint ignore-probes [-v|-verbose] [provider [name [objfile]]]`

`maint ignore-probes -reset`

Set or reset the ignore-probes filter. The `provider` arguments are as in `enable probes` and `disable probes` (see [enable probes](Static-Probe-Points.html#enable-probes)). Only supported for SystemTap probes.

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
