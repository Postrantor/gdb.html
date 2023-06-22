---
description: Command History (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Command History (Debugging with GDB)
lang: en
resource-type: document
title: Command History (Debugging with GDB)
---
::: header
Next: [Screen Size](Screen-Size.html#Screen-Size)]
:::

---

### 22.3 Command History

[GDB] command history facility.

[GDB] History library, a part of the Readline package, to provide the history facility. See [Using History Interactively](Using-History-Interactively.html#Using-History-Interactively), for the detailed description of the History library.

To issue a command to [GDB]'s notion of which command to repeat if RET is pressed on a line by itself.

The server prefix does not affect the recording of values into the value history; to print a value without recording it into the value history, use the `output` command instead of the `print` command.

Here is the description of [GDB] commands related to command history.

`set history filename [fname]`

Set the name of the [GDB] on MS-DOS) if this variable is not set.

The `GDBHISTFILE` environment variable is read after processing any [GDB] initialization files (see [Startup](Startup.html#Startup)) and after processing any commands passed using command line options (for example, `-ex`).

If the `fname` will neither try to load an existing history file, nor will it try to save the history on exit.

`set history save`

`set history save on`

Record command history in a file, whose name may be specified with the `set history filename` command. By default, this option is disabled. The command history will be recorded when [GDB] exits. If `set history filename` is set to the empty string then history saving is disabled, even when `set history save` is `on`.

`set history save off`

Don't record the command history into the file specified by `set history filename` when [GDB] exits.

`set history size size`

`set history size unlimited`

Set the number of commands which [GDB] keeps in the history list is unlimited.

The `GDBHISTSIZE` environment variable is read after processing any [GDB] initialization files (see [Startup](Startup.html#Startup)) and after processing any commands passed using command line options (for example, `-ex`).

`set history remove-duplicates count`

`set history remove-duplicates unlimited`

Control the removal of duplicate history entries in the command history list. If `count` is 0, then removal of duplicate history entries is disabled.

Only history entries added during the current session are considered for removal. This option is set to 0 by default.

History expansion assigns special meaning to the character [!]. See [Event Designators](Event-Designators.html#Event-Designators), for more details.

Since [!], even when history expansion is enabled.

The commands to control history expansion are:

`set history expansion on`
`set history expansion`

:

```
Enable history expansion. History expansion is off by default.
```

`set history expansion off`

:   Disable history expansion.

```

```

`show history`
`show history filename`
`show history save`
`show history size`
`show history expansion`

:   These commands display the state of the [GDB] history parameters. `show history` by itself displays all four states.

`show commands`

Display the last ten commands in the command history.

`show commands n`

Print ten commands centered on command number `n`.

`show commands +`

Print ten commands just after the commands last printed.

---

::: header
Next: [Screen Size](Screen-Size.html#Screen-Size)]
:::
