---
tip: translate by openai@2023-06-23 23:00:56
...
---
description: Guile Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Guile Commands (Debugging with GDB)
lang: en
resource-type: document
title: Guile Commands (Debugging with GDB)
---
::: header
Next: [Guile API](Guile-API.html#Guile-API)]
:::

---

#### 23.4.2 Guile Commands

[GDB] provides two commands for accessing the Guile interpreter:

`guile-repl`

`gr`


The `guile-repl` command can be used to start an interactive Guile prompt or *repl*. To return to [GDB] on an empty prompt). These commands do not take any arguments.

> `guile-repl` 命令可用于启动交互式 Guile 提示或 *repl*。在空提示符下返回[GDB]。这些命令不接受任何参数。

`guile [scheme-expression]`

`gu [scheme-expression]`

The `guile` command can be used to evaluate a Scheme expression.


If given an argument, [GDB] will pass the argument to the Guile interpreter for evaluation.

> 如果给出一个参数，[GDB] 将把参数传递给 Guile 解释器进行评估。

::: smallexample

```bash
(gdb) guile (display (+ 20 3)) (newline)
23
```

:::


The result of the Scheme expression is displayed using normal Guile rules.

> 结果使用正常的Guile规则显示出来。

::: smallexample

```bash
(gdb) guile (+ 20 3)
23
```

:::


If you do not provide an argument to `guile`, it will act as a multi-line command, like `define`. In this case, the Guile script is made up of subsequent command lines, given after the `guile` command. This command list is terminated using a line containing `end`. For example:

> 如果您没有为`guile`提供参数，它将充当多行命令，就像`define`一样。在这种情况下，Guile脚本由`guile`命令后面给出的后续命令行组成。使用包含`end`的行终止此命令列表。例如：

::: smallexample

```bash
(gdb) guile
>(display 23)
>(newline)
>end
23
```

:::

It is also possible to execute a Guile script from the [GDB] interpreter:

`source script-name`


:   The script name must end with '`.scm` must be configured to recognize the script language based on filename extension using the `script-extension` setting. See [Extending GDB](Extending-GDB.html#Extending-GDB).

> 脚本名称必须以`.scm`结尾，必须使用`script-extension`设置来识别基于文件扩展名的脚本语言。参见[扩展GDB](Extending-GDB.html#Extending-GDB)。

`guile (load "script-name")`


:   This method uses the `load` Guile function. It takes a string argument that is the name of the script to load. See the Guile documentation for a description of this function. (see [Loading](http://www.gnu.org/software/guile/manual/html_node/Loading.html#Loading) in GNU Guile Reference Manual).

> 这种方法使用`load`Guile函数。它接受一个字符串参数，即要加载的脚本的名称。有关此函数的详细描述，请参阅Guile文档（参见GNU Guile参考手册中的[加载](http://www.gnu.org/software/guile/manual/html_node/Loading.html#Loading)）。

---

::: header
Next: [Guile API](Guile-API.html#Guile-API)]
:::
