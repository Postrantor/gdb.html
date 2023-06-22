---
description: Python Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Python Commands (Debugging with GDB)
lang: en
resource-type: document
title: Python Commands (Debugging with GDB)
---
::: header
Next: [Python API](Python-API.html#Python-API)]
:::

---

#### 23.3.1 Python Commands

[GDB] provides two commands for accessing the Python interpreter, and one related setting:

`python-interactive [command]`

`pi [command]`

Without an argument, the `python-interactive` command can be used to start an interactive Python prompt. To return to [GDB] on an empty prompt).

Alternatively, a single-line Python command can be given as an argument and evaluated. If the command is an expression, the result will be printed; otherwise, nothing will be printed. For example:

::: smallexample

```bash
(gdb) python-interactive 2 + 3
5
```

:::

`python [command]`

`py [command]`

The `python` command can be used to evaluate Python code.

If given an argument, the `python` command will evaluate the argument as a Python command. For example:

::: smallexample

```bash
(gdb) python print 23
23
```

:::

If you do not provide an argument to `python`, it will act as a multi-line command, like `define`. In this case, the Python script is made up of subsequent command lines, given after the `python` command. This command list is terminated using a line containing `end`. For example:

::: smallexample

```bash
(gdb) python
>print 23
>end
23
```

:::

`set python print-stack`

By default, [GDB] will print only the message component of a Python exception when an error occurs in a Python script. This can be controlled using `set python print-stack`: if `full`, then full Python stack printing is enabled; if `none`, then Python stack and message printing is disabled; if `message`, the default, only the message component of the error is printed.

`set python ignore-environment [on|off]`

By default this option is '`off`.

If this option is set to '`on`'s startup process, then this option must be placed into the early initialization file (see [Initialization Files](Initialization-Files.html#Initialization-Files)) to have the desired effect.

This option is equivalent to passing `-E` to the real `python` executable.

`set python dont-write-bytecode [auto|on|off]`

When this option is '`off` files.

If this option is set to '`on`'s startup process, then this option must be placed into the early initialization file (see [Initialization Files](Initialization-Files.html#Initialization-Files)) to have the desired effect.

By default this option is set to '`auto`', the environment variable `PYTHONDONTWRITEBYTECODE` is examined to see if it should write out byte-code or not. `PYTHONDONTWRITEBYTECODE` is considered to be off/disabled either when set to the empty string or when the environment variable doesn't exist. All other settings, including those which don't seem to make sense, indicate that it's on/enabled.

This option is equivalent to passing `-B` to the real `python` executable.

It is also possible to execute a Python script from the [GDB] interpreter:

`source script-name`

:   The script name must end with '`.py` must be configured to recognize the script language based on filename extension using the `script-extension` setting. See [Extending GDB](Extending-GDB.html#Extending-GDB).

The following commands are intended to help debug [GDB] itself:

`set debug py-breakpoint on|off`

`show debug py-breakpoint`

When '`on`' by default.

`set debug py-unwind on|off`

`show debug py-unwind`

When '`on`' by default.

::: footnote

---

#### Footnotes

### [(19)](#DOCF19)

See the ENVIRONMENT VARIABLES section of `man 1 python` for a comprehensive list.
:::

---

::: header
Next: [Python API](Python-API.html#Python-API)]
:::
