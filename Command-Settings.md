---
description: Command Settings (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Command Settings (Debugging with GDB)
lang: en
resource-type: document
title: Command Settings (Debugging with GDB)
---
::: header
Next: [Completion](Completion.html#Completion)]
:::

---

### 3.2 Command Settings

Many commands change their behavior according to command-specific variables or settings. These settings can be changed with the `set` subcommands. For example, the `print` command (see [Examining Data](Data.html#Data)) prints arrays differently depending on settings changeable with the commands `set print elements NUMBER-OF-ELEMENTS` and `set print array-indexes`, among others.

You can change these settings to your preference in the gdbinit files loaded at [GDB] startup. See [Startup](Startup.html#Startup).

The settings can also be changed interactively during the debugging session. For example, to change the limit of array elements to print, you can do the following:

::: smallexample

```bash
(gdb) set print elements 10
(gdb) print some_array
$1 = 
```

:::

The above `set print elements 10` command changes the number of elements to print from the default of 200 to 10. If you only intend this limit of 10 to be used for printing `some_array`, then you must restore the limit back to 200, with `set print elements 200`.

Some commands allow overriding settings with command options. For example, the `print` command supports a number of options that allow overriding relevant global print settings as set by `set print` subcommands. See [print options](Data.html#print-options). The example above could be rewritten as:

::: smallexample

```bash
(gdb) print -elements 10 -- some_array
$1 = 
```

:::

Alternatively, you can use the `with` command to change a setting temporarily, for the duration of a command invocation.

`with setting [value] [-- command]`

`w setting [value] [-- command]`

Temporarily set `setting`.

`setting` is the value to assign to `setting` while running `command`.

If no `command` is provided, the last command executed is repeated.

If a `command` is provided, it must be preceded by a double dash (`--`) separator. This is required because some settings accept free-form arguments, such as expressions or filenames.

For example, the command

::: smallexample

```bash
(gdb) with print array on -- print some_array
```

:::

is equivalent to the following 3 commands:

::: smallexample

```bash
(gdb) set print array on
(gdb) print some_array
(gdb) set print array off
```

:::

The `with` command is particularly useful when you want to override a setting while running user-defined commands, or commands defined in Python or Guile. See [Extending GDB](Extending-GDB.html#Extending-GDB).

::: smallexample

```bash
(gdb) with print pretty on -- my_complex_command
```

:::

To change several settings for the same command, you can nest `with` commands. For example, `with language ada -- with print elements 10` temporarily changes the language to Ada and sets a limit of 10 elements to print for arrays and strings.

---

::: header
Next: [Completion](Completion.html#Completion)]
:::
