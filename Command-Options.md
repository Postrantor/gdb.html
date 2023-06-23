---
description: Command Options (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Command Options (Debugging with GDB)
lang: en
resource-type: document
title: Command Options (Debugging with GDB)
---
::: header
Next: [Help](Help.html#Help)]
:::

---

### 3.4 Command options

Some commands accept options starting with a leading dash. For example, `print -pretty`. Similarly to command names, you can abbreviate a [GDB] to fill out the rest of a word in an option (or to show you the alternatives available, if there is more than one possibility).

Some commands take raw input as argument. For example, the print command processes arbitrary expressions in any of the languages supported by [GDB]. With such commands, because raw input may start with a leading dash that would be confused with an option or any of its abbreviations, e.g. `print -p` (short for `print -pretty` or printing negative `p`?), if you specify any command option, then you must use a double-dash (`--`) delimiter to indicate the end of options.

Some options are described as accepting an argument which can be either `on` or `off`. These are known as *boolean options*. Similarly to boolean settings commands---`on` and `off` are the typical values, but any of `1`, `yes` and `enable` can also be used as "true" value, and any of `0`, `no` and `disable` can also be used as "false" value. You can also omit a "true" value, as it is implied by default.

For example, these are equivalent:

::: smallexample

```bash
(gdb) print -object on -pretty off -element unlimited -- *myptr
(gdb) p -o -p 0 -e u -- *myptr
```

:::

You can discover the set of options some command accepts by completing on `-` after the command name. For example:

::: smallexample

```bash
(gdb) print -TABTAB
-address         -max-depth               -object          -static-members
-array           -memory-tag-violations   -pretty          -symbol
-array-indexes   -nibbles                 -raw-values      -union
-elements        -null-stop               -repeats         -vtbl
```

:::

Completion will in some cases guide you with a suggestion of what kind of argument an option expects. For example:

::: smallexample

```bash
(gdb) print -elements TABTAB
NUMBER     unlimited
```

:::

Here, the option expects a number (e.g., `100`), not literal `NUMBER`. Such metasyntactical arguments are always presented in uppercase.

(For more on using the `print` command, see [Examining Data](Data.html#Data).)

---

::: header
Next: [Help](Help.html#Help)]
:::
