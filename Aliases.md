---
tip: translate by openai@2023-06-23 17:07:36
...
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

> 别名允许您为现有命令定义替代拼写。例如，如果在Python中定义了一个新的[GDB]命令（参见[Python]（Python.html#Python）），其名称较长，则有一个缩写版本可以减少输入量很方便。

[GDB]'.


Aliases are also used to provide shortened or more common versions of multi-word commands. For example, [GDB]' command.

> 别名也用于为多字命令提供缩写或更常用的版本。例如，[GDB] '命令。


You can define a new alias with the '`alias`' command.

> 你可以使用 'alias' 命令定义一个新的别名。

`alias [-a] [--] alias = command [default-args]`

`alias` must consist of letters, numbers, dashes and underscores.

`command` specifies the name of an existing command that is being aliased.

`command` cannot be an alias that has default arguments.


The '`-a`' option specifies that the new alias is an abbreviation of the command. Abbreviations are not used in command completion.

> '`-a`' 选项指定新的别名是命令的缩写。缩写不会用于命令补全。


The '`--` begins with a dash.

> “'”和“--”都以破折号开头。


You can specify `default-args` will be automatically added before the alias arguments typed explicitly on the command line.

> 你可以指定`默认参数`，它们会在命令行显式输入的别名参数之前自动添加。


For example, the below defines an alias `btfullall` that shows all local variables and all frame arguments:

> 例如，下面定义了一个别名`btfullall`，它显示所有本地变量和所有帧参数：

::: smallexample

```bash
(gdb) alias btfullall = backtrace -full -frame-arguments all
```

:::


For more information about `default-args`, see [Default Arguments](Command-aliases-default-args.html#Command-aliases-default-args).

> 如果要了解更多关于`default-args`的信息，请参阅[默认参数](Command-aliases-default-args.html#Command-aliases-default-args)。


Here is a simple example showing how to make an abbreviation of a command so that there is less to type. Suppose you were tired of typing '`disas`'. The following will accomplish this.

> 这里有一个简单的例子，展示如何缩写一个命令，以减少输入量。假设你厌倦了输入“disas”。以下操作将实现这一目的。

::: smallexample

```bash
(gdb) alias -a di = disas
```

:::

Note that aliases are different from user-defined commands. With a user-defined command, you also need to write documentation for it with the '`document`' command. An alias automatically picks up the documentation of the existing command.


Here is an example where we make '`elms`' command. This is to show that you can make an abbreviation of any part of a command.

> 这里有一个例子，我们创建了一个'elms'命令。这是为了表明你可以缩写任何命令的一部分。

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

> 允许在`command`中使用不易混淆的缩写命令，就像平常一样。

::: smallexample

```bash
(gdb) alias -a set pr elms = set p ele
```

:::


Finally, here is an example showing the creation of a one word alias for a more complex command. This creates alias '`spe`'.

> 最后，这里有一个示例，展示了如何为更复杂的命令创建一个单词别名。这将创建别名“spe”。

::: smallexample

```bash
(gdb) alias spe = set print elements
(gdb) spe 20
```

:::

---


• [Command aliases default args](Command-aliases-default-args.html#Command-aliases-default-args):        Default arguments for aliases

> • [命令别名默认参数](Command-aliases-default-args.html#Command-aliases-default-args)：默认参数为别名

---

---

::: header
Next: [Python](Python.html#Python)]
:::
