---
tip: translate by openai@2023-06-23 19:06:41
...
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

> 一些命令接受以连字符开头的选项。例如，`print -pretty`。与命令名称一样，您可以缩写[GDB]以填写选项中的其余部分（或者如果有多个可能性，显示可用的替代选项）。


Some commands take raw input as argument. For example, the print command processes arbitrary expressions in any of the languages supported by [GDB]. With such commands, because raw input may start with a leading dash that would be confused with an option or any of its abbreviations, e.g. `print -p` (short for `print -pretty` or printing negative `p`?), if you specify any command option, then you must use a double-dash (`--`) delimiter to indicate the end of options.

> 一些命令接受原始输入作为参数。例如，print 命令会处理[GDB]支持的任何一种语言中的任意表达式。对于这样的命令，由于原始输入可能以一个可能被误认为选项或其缩写的前导符号开头，例如 `print -p`（缩写为 `print -pretty` 或打印负 `p`？），如果您指定任何命令选项，则必须使用双破折号（`--`）作为选项结束的分隔符。


Some options are described as accepting an argument which can be either `on` or `off`. These are known as *boolean options*. Similarly to boolean settings commands---`on` and `off` are the typical values, but any of `1`, `yes` and `enable` can also be used as "true" value, and any of `0`, `no` and `disable` can also be used as "false" value. You can also omit a "true" value, as it is implied by default.

> 一些选项被描述为接受一个参数，参数可以是“on”或“off”。这些被称为*布尔选项*。类似于布尔设置命令--“on”和“off”是典型的值，但也可以使用“1”、“yes”和“enable”作为“true”值，也可以使用“0”、“no”和“disable”作为“false”值。你也可以省略“true”值，因为它是默认的。


For example, these are equivalent:

> 例如，这些是等价的：

::: smallexample

```bash
(gdb) print -object on -pretty off -element unlimited -- *myptr
(gdb) p -o -p 0 -e u -- *myptr
```

:::


You can discover the set of options some command accepts by completing on `-` after the command name. For example:

> 你可以通过在命令名称后面输入 `-` 来发现一些命令接受的选项集合。例如：

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

> 完成时有时会提供某个选项期望的参数类型的建议。例如：

::: smallexample

```bash
(gdb) print -elements TABTAB
NUMBER     unlimited
```

:::


Here, the option expects a number (e.g., `100`), not literal `NUMBER`. Such metasyntactical arguments are always presented in uppercase.

> 此处，该选项需要一个数字（例如`100`），而不是文字`NUMBER`。这种元语法参数通常以大写字母表示。


(For more on using the `print` command, see [Examining Data](Data.html#Data).)

> 对于如何使用`print`命令的更多信息，请参阅[检查数据](Data.html#Data)。

---

::: header
Next: [Help](Help.html#Help)]
:::
