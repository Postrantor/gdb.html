---
description: Set Breaks (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Set Breaks (Debugging with GDB)
lang: en
resource-type: document
title: Set Breaks (Debugging with GDB)
---
::: header
Next: [Set Watchpoints](Set-Watchpoints.html#Set-Watchpoints)]
:::

---

#### 5.1.1 Setting Breakpoints

Breakpoints are set with the `break` command (abbreviated `b`). The debugger convenience variable '`$bpnum`' records the number of the breakpoint you've set most recently:

::: smallexample

```bash
(gdb) b main
Breakpoint 1 at 0x11c6: file zeoes.c, line 24.
(gdb) p $bpnum
$1 = 1
```

:::

A breakpoint may be mapped to multiple code locations for example with inlined functions, Ada generics, C++ templates or overloaded function names. [GDB] then indicates the number of code locations in the breakpoint command output:

::: smallexample

```bash
(gdb) b some_func
Breakpoint 2 at 0x1179: some_func. (3 locations)
(gdb) p $bpnum
$2 = 2
(gdb)
```

:::

When your program stops on a breakpoint, the convenience variables '`$_hit_bpnum`' are respectively set to the number of the encountered breakpoint and the number of the breakpoint's code location:

::: smallexample

```bash
Thread 1 "zeoes" hit Breakpoint 2.1, some_func () at zeoes.c:8
8     printf("some func\n");
(gdb) p $_hit_bpnum
$5 = 2
(gdb) p $_hit_locno
$6 = 1
(gdb)
```

:::

Note that '`$_hit_bpnum`' is set to the breakpoint number **last set**.

If the encountered breakpoint has only one code location, '`$_hit_locno`' is set to 1:

::: smallexample

```bash
Breakpoint 1, main (argc=1, argv=0x7fffffffe018) at zeoes.c:24
24    if (argc > 1)
(gdb) p $_hit_bpnum
$3 = 1
(gdb) p $_hit_locno
$4 = 1
(gdb)
```

:::

The '`$_hit_bpnum` both disable the breakpoint.

You can also define aliases to easily disable the last hit location or last hit breakpoint:

::: smallexample

```bash
(gdb) alias lld = disable $_hit_bpnum.$_hit_locno
(gdb) alias lbd = disable $_hit_bpnum
```

:::

`break locspec`

:   Set a breakpoint at all the code locations in your program that result from resolving the given `locspec`. The breakpoint will stop your program just before it executes the instruction at the address of any of the breakpoint's code locations.

```
When using source languages that permit overloading of symbols, such as C++, a function name may refer to more than one symbol, and thus more than one place to break. See [Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions), for a discussion of that situation.

It is also possible to insert a breakpoint that will stop the program only if a specific thread (see [Thread-Specific Breakpoints](Thread_002dSpecific-Breakpoints.html#Thread_002dSpecific-Breakpoints)) or a specific task (see [Ada Tasks](Ada-Tasks.html#Ada-Tasks)) hits that breakpoint.
```

`break`

:   When called without any arguments, `break` sets a breakpoint at the next instruction to be executed in the selected stack frame (see [Examining the Stack](Stack.html#Stack)). In any selected frame but the innermost, this makes your program stop as soon as control returns to that frame. This is similar to the effect of a `finish` command in the frame inside the selected frame---except that `finish` does not leave an active breakpoint. If you use `break` without an argument in the innermost frame, [GDB] stops the next time it reaches the current location; this may be useful inside loops.

```
[GDB] normally ignores breakpoints when it resumes execution, until at least one instruction has been executed. If it did not do this, you would be unable to proceed past a breakpoint without first disabling the breakpoint. This rule applies whether or not the breakpoint already existed when your program stopped.
```

`break … if cond`

:   Set a breakpoint with condition `cond`' stands for one of the possible arguments described above (or no argument) specifying where to break. See [Break Conditions](Conditions.html#Conditions), for more information on breakpoint conditions.

```
The breakpoint may be mapped to multiple locations. If the breakpoint condition `cond` reports below that two of the three locations are disabled.

::: smallexample
``` smallexample
(gdb) break func if a == 10
warning: failed to validate condition at location 0x11ce, disabling:
  No symbol "a" in current context.
warning: failed to validate condition at location 0x11b6, disabling:
  No symbol "a" in current context.
Breakpoint 1 at 0x11b6: func. (3 locations)
```

:::

Locations that are disabled because of the condition are denoted by an uppercase `N` in the output of the `info breakpoints` command:

::: smallexample

```bash
(gdb) info breakpoints
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   <MULTIPLE>
        stop only if a == 10
1.1                         N*  0x00000000000011b6 in ...
1.2                         y   0x00000000000011c2 in ...
1.3                         N*  0x00000000000011ce in ...
(*): Breakpoint condition is invalid at this location.
```

:::

If the breakpoint condition `cond` refuses to define the breakpoint. For example, if variable `foo` is an undefined variable:

::: smallexample

```bash
(gdb) break func if foo
No symbol "foo" in current context.
```

:::

```

`break … -force-condition if cond`

:   There may be cases where the condition `cond` can be forced to define the breakpoint with the given condition expression instead of refusing it.

```

::: smallexample

```bash
(gdb) break func -force-condition if foo
warning: failed to validate condition at location 1, disabling:
  No symbol "foo" in current context.
warning: failed to validate condition at location 2, disabling:
  No symbol "foo" in current context.
warning: failed to validate condition at location 3, disabling:
  No symbol "foo" in current context.
Breakpoint 1 at 0x1158: test.c:18. (3 locations)
```

:::

This causes all the present locations where the breakpoint would otherwise be inserted, to be disabled, as seen in the example above. However, if there exist locations at which the condition is valid, the `-force-condition` keyword has no effect.

```

`tbreak args`

:   Set a breakpoint enabled only for one stop. The `args` are the same as for the `break` command, and the breakpoint is set in the same way, but the breakpoint is automatically deleted after the first time your program stops there. See [Disabling Breakpoints](Disabling.html#Disabling).

```

```

`hbreak args`

:   Set a hardware-assisted breakpoint. The `args` will use, see [set remote hardware-breakpoint-limit](Remote-Configuration.html#set-remote-hardware_002dbreakpoint_002dlimit).

```

```

`thbreak args`

:   Set a hardware-assisted breakpoint enabled only for one stop. The `args` are the same as for the `hbreak` command and the breakpoint is set in the same way. However, like the `tbreak` command, the breakpoint is automatically deleted after the first time your program stops there. Also, like the `hbreak` command, the breakpoint requires hardware support and some target hardware may not have this support. See [Disabling Breakpoints](Disabling.html#Disabling). See also [Break Conditions](Conditions.html#Conditions).

```

```

`rbreak regex`

:   Set breakpoints on all functions matching the regular expression `regex`. This command sets an unconditional breakpoint on all matches, printing a list of all breakpoints it set. Once these breakpoints are set, they are treated just like the breakpoints set with the `break` command. You can delete them, disable them, or make them conditional the same way as any other breakpoint.

```

In programs using different languages, [GDB]' (see [Set Language Automatically](Automatically.html#Automatically)) means to use the language of the breakpoint's function, other values mean to use the manually specified language (see [Set Language Manually](Manually.html#Manually)).

The syntax of the regular expression is the standard one used with tools like `grep`. Note that this is different from the syntax used by shells, so for instance `foo*` matches all functions that include an `fo` followed by zero or more `o` s. There is an implicit `.*` leading and trailing the regular expression you supply, so to match only functions that begin with `foo`, use `^foo`.

When debugging C++ programs, `rbreak` is useful for setting breakpoints on overloaded functions that are not members of any special classes.

The `rbreak` command can be used to set breakpoints in **all** the functions in a program, like this:

::: smallexample

```bash
(gdb) rbreak .
```

:::

```

`rbreak file:regex`

:   If `rbreak` is called with a filename qualification, it limits the search for functions matching the given regular expression to the specified `file`. This can be used, for example, to set breakpoints on every function in a given file:

```

::: smallexample

```bash
(gdb) rbreak file.c:.
```

:::

The colon separating the filename qualifier from the regex may optionally be surrounded by spaces.

```

`info breakpoints [list…]`
`info break [list…]`

:   Print a table of all breakpoints, watchpoints, and catchpoints set and not deleted. Optional argument `n` means print information only about the specified breakpoint(s) (or watchpoint(s) or catchpoint(s)). For each breakpoint, following columns are printed:

```

*Breakpoint Numbers*
*Type*

:   Breakpoint, watchpoint, or catchpoint.

*Disposition*

:   Whether the breakpoint is marked to be disabled or deleted when hit.

*Enabled or Disabled*

:   Enabled breakpoints are marked with '`y`' marks breakpoints that are not enabled.

*Address*

:   Where the breakpoint is in your program, as a memory address. For a pending breakpoint whose address is not yet known, this field will contain '`<PENDING>`' in this field---see below for details.

*What*

:   Where the breakpoint is in the source for your program, as a file and line number. For a pending breakpoint, the original string passed to the breakpoint command will be listed as it cannot be resolved until the appropriate shared library is loaded in the future.

If a breakpoint is conditional, there are two evaluation modes: "host" and "target". If mode is "host", breakpoint condition evaluation is done by [GDB] on the host's side. If it is "target", then the condition is evaluated by the target. The `info break` command shows the condition on the line following the affected breakpoint, together with its condition evaluation mode in between parentheses.

Breakpoint commands, if any, are listed after that. A pending breakpoint is allowed to have a condition specified for it. The condition is not parsed for validity until a shared library is loaded that allows the pending breakpoint to resolve to a valid location.

`info break` with a breakpoint number `n` as argument lists only that breakpoint. The convenience variable `$_` and the default examining-address for the `x` command are set to the address of the last breakpoint listed (see [Examining Memory](Memory.html#Memory)).

`info break` displays a count of the number of times the breakpoint has been hit. This is especially useful in conjunction with the `ignore` command. You can ignore a large number of breakpoint hits, look at the breakpoint info to see how many times the breakpoint was hit, and then run again, ignoring one less than that number. This will get you quickly to the last hit of that breakpoint.

For a breakpoints with an enable count (xref) greater than 1, `info break` also displays that count.

```

[GDB] allows you to set any number of breakpoints at the same place in your program. There is nothing silly or meaningless about this. When the breakpoints are conditional, this is even useful (see [Break Conditions](Conditions.html#Conditions)).



It is possible that a single logical breakpoint is set at several code locations in your program. See [Location Specifications](Location-Specifications.html#Location-Specifications), for examples.

A breakpoint with multiple code locations is displayed in the breakpoint table using several rows---one header row, followed by one row for each code location. The header row has '`<MULTIPLE>`.

For example:

::: smallexample

```bash
Num     Type           Disp Enb  Address    What
1       breakpoint     keep y    <MULTIPLE>
        stop only if i==1
        breakpoint already hit 1 time
1.1                         y    0x080486a2 in void foo<int>() at t.cc:8
1.2                         y    0x080486ca in void foo<double>() at t.cc:8
```

:::

You cannot delete the individual locations from a breakpoint. However, each location can be individually enabled or disabled by passing `breakpoint-number` acts on all the locations in the range (inclusive). Disabling or enabling the parent breakpoint (see [Disabling](Disabling.html#Disabling)) affects all of the locations that belong to that breakpoint.

Locations that are enabled while their parent breakpoint is disabled won't trigger a break, and are denoted by `y-` in the `Enb` column. For example:

::: smallexample

```bash
(gdb) info breakpoints
Num     Type           Disp Enb Address            What
1       breakpoint     keep n   <MULTIPLE>
1.1                         y-  0x00000000000011b6 in ...
1.2                         y-  0x00000000000011c2 in ...
1.3                         n   0x00000000000011ce in ...
```

:::

It's quite common to have a breakpoint inside a shared library. Shared libraries can be loaded and unloaded explicitly, and possibly repeatedly, as the program is executed. To support this use case, [GDB] will ask you if you want to set a so called *pending breakpoint*---breakpoint whose address is not yet resolved.

After the program is run, whenever a new shared library is loaded, [GDB] reevaluates all the breakpoints. When a newly loaded shared library contains the symbol or line referred to by some pending breakpoint, that breakpoint is resolved and becomes an ordinary breakpoint. When a library is unloaded, all breakpoints that refer to its symbols or source lines become pending again.

This logic works for breakpoints with multiple locations, too. For example, if you have a breakpoint in a C++ template function, and a newly loaded shared library has an instantiation of that template, a new location is added to the list of locations for the breakpoint.

Except for having unresolved address, pending breakpoints do not differ from regular breakpoints. You can set conditions or commands, enable and disable them and perform other breakpoint operations.

[GDB]' command cannot resolve the location spec to any code location in your program (see [Location Specifications](Location-Specifications.html#Location-Specifications)):

`set breakpoint pending auto`

:   This is the default behavior. When [GDB] cannot resolve the location spec, it queries you whether a pending breakpoint should be created.

`set breakpoint pending on`

:   This indicates that when [GDB] cannot resolve the location spec, it should create a pending breakpoint without confirmation.

`set breakpoint pending off`

:   This indicates that pending breakpoints are not to be created. If [GDB] cannot resolve the location spec, it aborts the breakpoint creation with an error. This setting does not affect any pending breakpoints previously created.

`show breakpoint pending`

:   Show the current behavior setting for creating pending breakpoints.

The settings above only affect the `break` command and its variants. Once a breakpoint is set, it will be automatically updated as shared libraries are loaded and unloaded.

For some targets, [GDB] will always use hardware breakpoints.

You can control this automatic behaviour with the following commands:

`set breakpoint auto-hw on`

:   This is the default behavior. When [GDB] sets a breakpoint, it will try to use the target memory map to decide if software or hardware breakpoint must be used.

`set breakpoint auto-hw off`

:   This indicates [GDB] will warn when trying to set software breakpoint at a read-only address.

[GDB] restores the original instructions. This behaviour guards against leaving breakpoints inserted in the target should gdb abrubptly disconnect. However, with slow remote targets, inserting and removing breakpoint can reduce the performance. This behavior can be controlled with the following commands::

`set breakpoint always-inserted off`

:   All breakpoints, including newly added by the user, are inserted in the target only when the target is resumed. All breakpoints are removed from the target when it stops. This is the default mode.

`set breakpoint always-inserted on`

:   Causes all breakpoints to be inserted in the target at all times. If the user adds a new breakpoint, or changes an existing breakpoint, the breakpoints in the target are updated immediately. A breakpoint is removed from the target only when breakpoint itself is deleted.

[GDB] handles conditional breakpoints by evaluating these conditions when a breakpoint breaks. If the condition is true, then the process being debugged stops, otherwise the process is resumed.

If the target supports evaluating conditions on its end, [GDB] may download the breakpoint, together with its conditions, to it.

This feature can be controlled via the following commands:

`set breakpoint condition-evaluation host`

:   This option commands [GDB] to evaluate the breakpoint conditions on the host's side. Unconditional breakpoints are sent to the target which in turn receives the triggers and reports them back to GDB for condition evaluation. This is the standard evaluation mode.

`set breakpoint condition-evaluation target`

:   This option commands [GDB].

`set breakpoint condition-evaluation auto`

:   This is the default mode. If the target supports evaluating breakpoint conditions on its end, [GDB] will fallback to evaluating all these conditions on the host's side.

[GDB]' (see [maint info breakpoints](Maintenance-Commands.html#maint-info-breakpoints)).

---

::: header
Next: [Set Watchpoints](Set-Watchpoints.html#Set-Watchpoints)]
:::
