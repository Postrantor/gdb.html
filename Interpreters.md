---
tip: translate by openai@2023-06-23 23:33:02
...
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

> [GDB]支持多种命令解释器，并提供一些命令基础设施，以允许用户或用户界面作者在解释器之间切换或在其他解释器中运行命令。

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

> 你可以在当前的解释器中使用适当的命令在任何解释器中执行命令。如果你正在运行控制台解释器，只需使用`interpreter-exec`命令即可：

::: smallexample

```bash
interpreter-exec mi "-data-list-register-names"
```

:::

[GDB/MI] version 2 (or greater).


Note that `interpreter-exec` only changes the interpreter for the duration of the specified command. It does not change the interpreter permanently.

> 注意，`interpreter-exec`只会暂时改变指定命令的解释器，而不会永久改变解释器。


Although you may only choose a single interpreter at startup, it is possible to run an independent interpreter on a specified input/output device (usually a tty).

> 尽管你可能只能在启动时选择一个解释器，但可以在指定的输入/输出设备（通常是tty）上运行独立的解释器。


For example, consider a debugger GUI or IDE that wants to provide a [GDB] using the separate MI interpreter.

> 例如，考虑一个想要提供[GDB]使用单独的MI解释器的调试器GUI或IDE。


To start a new secondary *user interface* running MI, use the `new-ui` command:

> 要启动一个新的次级用户界面运行MI，请使用`new-ui`命令：

::: smallexample

```bash
new-ui interpreter tty
```

:::


The `interpreter` parameter specifies the name of the bidirectional file the interpreter uses for input/output, usually the name of a pseudoterminal slave on Unix systems. For example:

> 参数`interpreter`指定双向文件的名称，该文件用于输入/输出，通常是Unix系统上伪终端从属的名称。例如：

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
