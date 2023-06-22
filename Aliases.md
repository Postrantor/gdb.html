---
description: Aliases (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Aliases (Debugging with GDB)
lang: en
resource-type: document
title: Aliases (Debugging with GDB)
---
::: header
Next: [Python](Python.html#Python)]
:::

---

### 23.2 Command Aliases

Aliases allow you to define alternate spellings for existing commands. For example, if a new [GDB] command defined in Python (see [Python](Python.html#Python)) has a long name, it is handy to have an abbreviated version of it that involves less typing.

[GDB]'.

Aliases are also used to provide shortened or more common versions of multi-word commands. For example, [GDB]' command.

You can define a new alias with the '`alias`' command.

`alias [-a] [--] alias = command [default-args]`

`alias` must consist of letters, numbers, dashes and underscores.

`command` specifies the name of an existing command that is being aliased.

`command` cannot be an alias that has default arguments.

The '`-a`' option specifies that the new alias is an abbreviation of the command. Abbreviations are not used in command completion.

The '`--` begins with a dash.

You can specify `default-args` will be automatically added before the alias arguments typed explicitly on the command line.

For example, the below defines an alias `btfullall` that shows all local variables and all frame arguments:

::: smallexample

```bash
(gdb) alias btfullall = backtrace -full -frame-arguments all
```

:::

For more information about `default-args`, see [Default Arguments](Command-aliases-default-args.html#Command-aliases-default-args).

Here is a simple example showing how to make an abbreviation of a command so that there is less to type. Suppose you were tired of typing '`disas`'. The following will accomplish this.

::: smallexample

```bash
(gdb) alias -a di = disas
```

:::

Note that aliases are different from user-defined commands. With a user-defined command, you also need to write documentation for it with the '`document`' command. An alias automatically picks up the documentation of the existing command.

Here is an example where we make '`elms`' command. This is to show that you can make an abbreviation of any part of a command.

::: smallexample

```bash
(gdb) alias -a set print elms = set print elements
(gdb) alias -a show print elms = show print elements
(gdb) set p elms 200
(gdb) show p elms
Limit on string chars or array elements to print is 200.
```

:::

Note that if you are defining an alias of a '`set`' command, then you need to define the latter separately.

Unambiguously abbreviated commands are allowed in `command`, just as they are normally.

::: smallexample

```bash
(gdb) alias -a set pr elms = set p ele
```

:::

Finally, here is an example showing the creation of a one word alias for a more complex command. This creates alias '`spe`'.

::: smallexample

```bash
(gdb) alias spe = set print elements
(gdb) spe 20
```

:::

---

• [Command aliases default args](Command-aliases-default-args.html#Command-aliases-default-args):        Default arguments for aliases

---

---

::: header
Next: [Python](Python.html#Python)]
:::
