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

`set exec-done-display`

Turns on or off the notification of asynchronous commands' completion. When on, [GDB]

`show exec-done-display`

Displays the current setting of asynchronous command completion notification.

`set debug aarch64`

Turns on or off display of debugging messages related to ARM AArch64. The default is off.

`show debug aarch64`

Displays the current state of displaying debugging messages related to ARM AArch64.

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

`set debug amd-dbgapi`

`show debug amd-dbgapi`

The '`set debug amd-dbgapi`' command displays the current setting. See [set debug amd-dbgapi](#set-debug-amd_002ddbgapi).

`set debug check-physname`

Check the results of the "physname" computation. When reading DWARF debugging information for C++, [GDB] to compute the names both ways and display any discrepancies.

`show debug check-physname`

Show the current state of "physname" checking.

`set debug coff-pe-read`

Control display of debugging messages related to reading of COFF/PE exported symbols. The default is off.

`show debug coff-pe-read`

Displays the current state of displaying debugging messages related to reading of COFF/PE exported symbols.

`set debug dwarf-die`

Dump DWARF DIEs after they are read in. The value is the number of nesting levels to print. A value of zero turns off the display.

`show debug dwarf-die`

Show the current state of DWARF DIE debugging.

`set debug dwarf-line`

Turns on or off display of debugging messages related to reading DWARF line tables. The default is 0 (off). A value of 1 provides basic information. A value greater than 1 provides more verbose information.

`show debug dwarf-line`

Show the current state of DWARF line table debugging.

`set debug dwarf-read`

Turns on or off display of debugging messages related to reading DWARF debug info. The default is 0 (off). A value of 1 provides basic information. A value greater than 1 provides more verbose information.

`show debug dwarf-read`

Show the current state of DWARF reader debugging.

`set debug displaced`

Turns on or off display of [GDB] debugging info for the displaced stepping support. The default is off.

`show debug displaced`

Displays the current state of displaying [GDB] debugging info related to displaced stepping.

`set debug event`

Turns on or off display of [GDB] event debugging info. The default is off.

`show debug event`

Displays the current state of displaying [GDB] event debugging info.

`set debug event-loop`

Controls output of debugging info about the event loop. The possible values are '`off`' (shows all debugging info except those about UI-related events).

`show debug event-loop`

Shows the current state of displaying debugging info about the event loop.

`set debug expression`

Turns on or off display of debugging info about [GDB] expression parsing. The default is off.

`show debug expression`

Displays the current state of displaying debugging info about [GDB] expression parsing.

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

`show debug fortran-array-slicing`

Displays the current state of displaying [GDB] Fortran array slicing debugging info.

`set debug frame`

Turns on or off display of [GDB] frame debugging info. The default is off.

`show debug frame`

Displays the current state of displaying [GDB] frame debugging info.

`set debug gnu-nat`

Turn on or off debugging messages from the [GNU]/Hurd debug support.

`show debug gnu-nat`

Show the current state of [GNU]/Hurd debugging messages.

`set debug infrun`

Turns on or off display of [GDB] contains GDB's runtime state machine used for implementing operations such as single-stepping the inferior.

`show debug infrun`

Displays the current state of [GDB] inferior debugging.

`set debug infcall`

Turns on or off display of debugging info related to inferior function calls made by [GDB].

`show debug infcall`

Displays the current state of [GDB] inferior function call debugging.

`set debug jit`

Turn on or off debugging messages from JIT debug support.

`show debug jit`

Displays the current state of [GDB] JIT debugging.

`set debug linux-nat [on|off]`

Turn on or off debugging messages from the Linux native target debug support.

`show debug linux-nat`

Show the current state of Linux native target debugging messages.

`set debug linux-namespaces`

Turn on or off debugging messages from the Linux namespaces debug support.

`show debug linux-namespaces`

Show the current state of Linux namespaces debugging messages.

`set debug mach-o`

Control display of debugging messages related to Mach-O symbols processing. The default is off.

`show debug mach-o`

Displays the current state of displaying debugging messages related to reading of COFF/PE exported symbols.

`set debug notification`

Turn on or off debugging messages about remote async notification. The default is off.

`show debug notification`

Displays the current state of remote async notification debugging messages.

`set debug observer`

Turns on or off display of [GDB] observer debugging. This includes info such as the notification of observable events.

`show debug observer`

Displays the current state of observer debugging.

`set debug overload`

Turns on or off display of [GDB] C++ overload debugging info. This includes info such as ranking of functions, etc. The default is off.

`show debug overload`

Displays the current state of displaying [GDB] C++ overload debugging info.

`set debug parser`

Turns on or off the display of expression parser debugging output. Internally, this sets the `yydebug` variable in the expression parser. See [Tracing Your Parser](http://www.gnu.org/software/bison/manual/html_node/Tracing.html#Tracing) in Bison, for details. The default is off.

`show debug parser`

Show the current state of expression parser debugging.

`set debug remote`

Turns on or off display of reports on all packets sent back and forth across the serial line to the remote machine. The info is printed on the [GDB] standard output stream. The default is off.

`show debug remote`

Displays the state of display of remote packets.

`set debug remote-packet-max-chars`

Sets the maximum number of characters to display for each remote packet when `set debug remote` is on. This is useful to prevent [GDB] from displaying lengthy remote packets and polluting the console.

The default value is `512`, which means [GDB] will truncate each remote packet after 512 bytes.

Setting this option to `unlimited` will disable truncation and will output the full length of the remote packets.

`show debug remote-packet-max-chars`

Displays the number of bytes to output for remote packet debugging.

`set debug separate-debug-file`

Turns on or off display of debug output about separate debug file search.

`show debug separate-debug-file`

Displays the state of separate debug file search debug output.

`set debug serial`

Turns on or off display of [GDB] serial debugging info. The default is off.

`show debug serial`

Displays the current state of displaying [GDB] serial debugging info.

`set debug solib`

Turns on or off display of debugging messages related to shared libraries. The default is off.

`show debug solib`

Show the current state of solib debugging messages.

`set debug symbol-lookup`

Turns on or off display of debugging messages related to symbol lookup. The default is 0 (off). A value of 1 provides basic information. A value greater than 1 provides more verbose information.

`show debug symbol-lookup`

Show the current state of symbol lookup debugging messages.

`set debug symfile`

Turns on or off display of debugging messages related to symbol file functions. The default is off. See [Files](Files.html#Files).

`show debug symfile`

Show the current state of symbol file debugging messages.

`set debug symtab-create`

Turns on or off display of debugging messages related to symbol table creation. The default is 0 (off). A value of 1 provides basic information. A value greater than 1 provides more verbose information.

`show debug symtab-create`

Show the current state of symbol table creation debugging.

`set debug target`

Turns on or off display of [GDB] target debugging info. This info includes what is going on at the target level of GDB, as it happens. The default is 0. Set it to 1 to track events, and to 2 to also track the value of large memory transfers.

`show debug target`

Displays the current state of displaying [GDB] target debugging info.

`set debug timestamp`

Turns on or off display of timestamps with [GDB] debugging info. When enabled, seconds and microseconds are displayed before each debugging message.

`show debug timestamp`

Displays the current state of displaying timestamps with [GDB] debugging info.

`set debug varobj`

Turns on or off display of [GDB] variable object debugging info. The default is off.

`show debug varobj`

Displays the current state of displaying [GDB] variable object debugging info.

`set debug xml`

Turn on or off debugging messages for built-in XML parsers.

`show debug xml`

Displays the current state of XML debugging messages.

---

::: header
Next: [Other Misc Settings](Other-Misc-Settings.html#Other-Misc-Settings)]
:::
