---
description: Shell Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Shell Commands (Debugging with GDB)
lang: en
resource-type: document
title: Shell Commands (Debugging with GDB)
---
::: header
Next: [Logging Output](Logging-Output.html#Logging-Output)]
:::

---

### 2.3 Shell Commands

If you need to execute occasional shell commands during your debugging session, there is no need to leave or suspend [GDB]; you can just use the `shell` command.

`shell command-string`

`!command-string`

Invoke a shell to execute `command-string` on MS-DOS, etc.).

You may also invoke shell commands from expressions, using the `$_shell` convenience function. See [\$_shell convenience function](Convenience-Funs.html#g_t_0024_005fshell-convenience-function).

The utility `make` is often needed in development environments. You do not have to use the `shell` command for this purpose in [GDB]:

`make make-args`

Execute the `make` program with the specified arguments. This is equivalent to '`shell make make-args`'.

`pipe [command] | shell_command`

`| [command] | shell_command`

`pipe -d delim command delim shell_command`

`| -d delim command delim shell_command`

Executes `command` is provided, the last command executed is repeated.

In case the `command`.

Example:

::: smallexample

```bash
(gdb) p var
$1 = {
  black = 144,
  red = 233,
  green = 377,
  blue = 610,
  white = 987
}
```

```bash
(gdb) pipe p var|wc
      7      19      80
(gdb) |p var|wc -l
7
```

```bash
(gdb) p /x var
$4 = {
  black = 0x90,
  red = 0xe9,
  green = 0x179,
  blue = 0x262,
  white = 0x3db
}
(gdb) ||grep red
  red => 0xe9,
```

```bash
(gdb) | -d ! echo this contains a | char\n ! sed -e 's/|/PIPE/'
this contains a PIPE char
(gdb) | -d xxx echo this contains a | char!\n xxx sed -e 's/|/PIPE/'
this contains a PIPE char!
(gdb)
```

:::

The convenience variables `$_shell_exitcode` and `$_shell_exitsignal` can be used to examine the exit status of the last shell command launched by `shell`, `make`, `pipe` and `|`. See [Convenience Variables](Convenience-Vars.html#Convenience-Vars).

---

::: header
Next: [Logging Output](Logging-Output.html#Logging-Output)]
:::
