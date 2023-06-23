---
description: Interpreters (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Interpreters (Debugging with GDB)
lang: en
resource-type: document
title: Interpreters (Debugging with GDB)
---
::: header
Next: [TUI](TUI.html#TUI)]
:::

---

## 24 Command Interpreters

[GDB] supports multiple command interpreters, and some command infrastructure to allow users or user interface writers to switch between interpreters or run commands in other interpreters.

[GDB]). This manual describes both of these interfaces in great detail.

By default, [GDB] startup options. Defined interpreters include:

`console`

:

```
The traditional console or command-line interpreter. This is the most often used interpreter with [GDB] will use this interpreter.
```

`dap`

:

```
When [GDB] extensions to the protocol.
```

`mi`

:

```
The newest [GDB/MI] Interface](GDB_002fMI.html#GDB_002fMI).
```

`mi3`

:

```
The [GDB/MI] 9.1.
```

`mi2`

:

```
The [GDB/MI] 6.0.
```

You may execute commands in any interpreter from the current interpreter using the appropriate command. If you are running the console interpreter, simply use the `interpreter-exec` command:

::: smallexample

```bash
interpreter-exec mi "-data-list-register-names"
```

:::

[GDB/MI] version 2 (or greater).

Note that `interpreter-exec` only changes the interpreter for the duration of the specified command. It does not change the interpreter permanently.

Although you may only choose a single interpreter at startup, it is possible to run an independent interpreter on a specified input/output device (usually a tty).

For example, consider a debugger GUI or IDE that wants to provide a [GDB] using the separate MI interpreter.

To start a new secondary *user interface* running MI, use the `new-ui` command:

::: smallexample

```bash
new-ui interpreter tty
```

:::

The `interpreter` parameter specifies the name of the bidirectional file the interpreter uses for input/output, usually the name of a pseudoterminal slave on Unix systems. For example:

::: smallexample

```bash
(gdb) new-ui mi /dev/pts/9
```

:::

runs an MI interpreter on `/dev/pts/9`.

---

::: header
Next: [TUI](TUI.html#TUI)]
:::
