---
tip: translate by openai@2023-06-24 10:13:26
...
---
description: Basic Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Basic Guile (Debugging with GDB)
lang: en
resource-type: document
title: Basic Guile (Debugging with GDB)
---
::: header
Next: [Guile Configuration](Guile-Configuration.html#Guile-Configuration)]
:::

---

#### 23.4.3.1 Basic Guile


At startup, [GDB]'s output-paging streams. A Guile program which outputs to one of these streams may have its output interrupted by the user (see [Screen Size](Screen-Size.html#Screen-Size)). In this situation, a Guile `signal` exception is thrown with value `SIGINT`.

> 在启动时，GDB的输出分页流。一个Guile程序将输出重定向到其中一个流时，可能会被用户中断（参见屏幕尺寸）。在这种情况下，Guile将抛出一个`signal`异常，其值为`SIGINT`。

Guile's history mechanism uses the same naming as [GDB].

[GDB] thread.


Some care must be taken when writing Guile code to run in [GDB]. Two things are worth noting in particular:

> 写Guile代码运行在GDB时需要注意一些事情。特别需要注意的有两件事：

- [GDB] will most likely stop working correctly. Note that it is unfortunately common for GUI toolkits to install a `SIGCHLD` handler.
- [GDB] takes care to mark its internal file descriptors as close-on-exec. However, this cannot be done in a thread-safe way on all platforms. Your Guile programs should be aware of this and should both create new file descriptors with the close-on-exec flag set and arrange to close unneeded file descriptors before starting a child process.


[GDB] leaves the choice of how the `gdb` module is imported to the user. To simplify interactive use, it is recommended to add one of the following to your \~/.gdbinit.

> [GDB] 将如何导入`gdb`模块的选择留给用户。为了简化交互使用，建议您将以下内容之一添加到您的\~/.gdbinit中。

::: smallexample

```bash
guile (use-modules (gdb))
```

:::

::: smallexample

```bash
guile (use-modules ((gdb) #:renamer (symbol-prefix-proc 'gdb:)))
```

:::


Which one to choose depends on your preference. The second one adds `gdb:` as a prefix to all module functions and variables.

> 这一个选择取决于你的偏好。第二个会在所有模块函数和变量前加上`gdb:`前缀。


The rest of this manual assumes the `gdb` module has been imported without any prefix. See the Guile documentation for `use-modules` for more information (see [Using Guile Modules](http://www.gnu.org/software/guile/manual/html_node/Using-Guile-Modules.html#Using-Guile-Modules) in GNU Guile Reference Manual).

> 本手册的其余部分假定`gdb`模块已经被无前缀导入。有关更多信息，请参阅Guile文档中的`use-modules`（参见GNU Guile参考手册中的[使用Guile模块](http://www.gnu.org/software/guile/manual/html_node/Using-Guile-Modules.html#Using-Guile-Modules)）。

Example:

::: smallexample

```bash
(gdb) guile (value-type (make-value 1))
ERROR: Unbound variable: value-type
Error while executing Scheme code.
(gdb) guile (use-modules (gdb))
(gdb) guile (value-type (make-value 1))
int
(gdb)
```

:::

The `(gdb)` module provides these basic Guile functions.

*


:   Evaluate `command` runs, it is translated as described in [Guile Exception Handling](Guile-Exception-Handling.html#Guile-Exception-Handling).

> 评估`command`运行，它按照[Guile异常处理](Guile-Exception-Handling.html#Guile-Exception-Handling)中的描述进行翻译。

```
`from-tty` ought to consider this command as having originated from the user invoking it interactively. It must be a boolean value. If omitted, it defaults to `#f`.

By default, any output produced by `command` virtual terminal will be temporarily set to unlimited width and height, and its pagination will be disabled; see [Screen Size](Screen-Size.html#Screen-Size).
```

```
<!-- -->
```

Scheme Procedure: **history-ref** *number*


:   Return a value from [GDB] doesn't exist in the value history, a `gdb:error` exception will be raised.

> 如果从[GDB]返回的值不存在于值历史中，将引发一个`gdb:error`异常。

```
If no exception is raised, the return value is always an instance of `<gdb:value>` (see [Values From Inferior In Guile](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile)).

*Note:* [GDB]'s command line and `$1` from Guile's history contains the result of evaluating an expression from Guile's command line.
```

```
<!-- -->
```

Scheme Procedure: **history-append!** *value*

:   Append `value`'s value history. Return its index in the history.

```
Putting into history values returned by Guile extensions will allow the user convenient access to those values via CLI history facilities.
```

```
<!-- -->
```

Scheme Procedure: **parse-and-eval** *expression*

:   Parse `expression` must be a string.

```
This function can be useful when implementing a new command (see [Commands In Guile](Commands-In-Guile.html#Commands-In-Guile)), as it provides a way to parse the command's arguments as an expression. It is also is useful when computing values. For example, it is the only way to get the value of a convenience variable (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) as a `<gdb:value>`.
```

---

::: header
Next: [Guile Configuration](Guile-Configuration.html#Guile-Configuration)]
:::
