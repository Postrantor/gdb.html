---
tip: translate by openai@2023-06-23 19:00:29
...
---
description: Command aliases default args (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Command aliases default args (Debugging with GDB)
lang: en
resource-type: document
title: Command aliases default args (Debugging with GDB)
---
::: header

Up: [Aliases](Aliases.html#Aliases)]

> 上：[别名](Aliases.html#Aliases)
:::

---

#### 23.2.1 Default Arguments


You can tell [GDB] to always prepend some default arguments to the list of arguments provided explicitly by the user when using a user-defined alias.

> 你可以告诉GDB在使用用户定义的别名时，总是在用户明确提供的参数列表之前添加一些默认参数。


If you repeatedly use the same arguments or options for a command, you can define an alias for this command and tell [GDB].

> 如果你反复使用同一个命令的相同参数或选项，你可以为这个命令定义一个别名，并告诉[GDB]。


For example, if you often use the command `thread apply all` specifying to work on the threads in ascending order and to continue in case it encounters an error, you can tell [GDB] to automatically preprend the `-ascending` and `-c` options by using:

> 例如，如果您经常使用指定以升序处理线程并在遇到错误时继续的命令`thread apply all`，您可以使用以下方法告诉[GDB]自动附加`-ascending`和`-c`选项：

::: smallexample

```bash
(gdb) alias thread apply asc-all = thread apply all -ascending -c
```

:::


Once you have defined this alias with its default args, any time you type the `thread apply asc-all` followed by `some arguments`, [GDB] will execute `thread apply all -ascending -c some arguments`.

> 一旦您使用默认参数定义了这个别名，每次输入`thread apply asc-all`后跟`一些参数`时，[GDB]将执行`thread apply all -ascending -c 一些参数`。


To have even less to type, you can also define a one word alias:

> 可以进一步减少输入，您还可以定义一个单词别名：

::: smallexample

```bash
(gdb) alias t_a_c = thread apply all -ascending -c
```

:::


As usual, unambiguous abbreviations can be used for `alias`.

> 通常，可以使用清晰的缩写来作为“别名”。


The different aliases of a command do not share their default args. For example, you define a new alias `bt_ALL` showing all possible information and another alias `bt_SMALL` showing very limited information using:

> 命令的不同别名不会共享它们的默认参数。例如，您使用以下方式定义一个显示所有可能信息的新别名`bt_ALL`和另一个显示非常有限信息的别名`bt_SMALL`：

::: smallexample

```bash
(gdb) alias bt_ALL = backtrace -entry-values both -frame-arg all \
   -past-main -past-entry -full
(gdb) alias bt_SMALL = backtrace -entry-values no -frame-arg none \
   -past-main off -past-entry off
```

:::


(For more on using the `alias` command, see [Aliases](Aliases.html#Aliases).)

> 对于使用`alias`命令的更多信息，请参阅[别名](Aliases.html#Aliases)。


Default args are not limited to the arguments and options of `command` accepts such a nested command as argument. For example, the below defines `faalocalsoftype` that lists the frames having locals of a certain type, together with the matching local vars:

> 默认参数不仅限于`command`接受的参数和选项，还可以接受嵌套命令作为参数。例如，下面定义的`faalocalsoftype`可以列出具有某种类型的局部变量的框架，以及匹配的局部变量：

::: smallexample

```bash
(gdb) alias faalocalsoftype = frame apply all info locals -q -t
(gdb) faalocalsoftype int
#1  0x55554f5e in sleeper_or_burner (v=0xdf50) at sleepers.c:86
i = 0
ret = 21845
```

:::


This is also very useful to define an alias for a set of nested `with` commands to have a particular combination of temporary settings. For example, the below defines the alias `pp10` that pretty prints an expression argument, with a maximum of 10 elements if the expression is a string or an array:

> 这也非常有用，可以为一组嵌套的“with”命令定义别名，以便具有特定的临时设置组合。例如，下面定义了别名“pp10”，它可以根据表达式参数进行漂亮的打印，如果表达式是字符串或数组，则最多可以有10个元素：

::: smallexample

```bash
(gdb) alias pp10 = with print pretty -- with print elements 10 -- print
```

:::


This defines the alias `pp10` as being a sequence of 3 commands. The first part `with print pretty --` temporarily activates the setting `set print pretty`, then launches the command that follows the separator `--`. The command following the first part is also a `with` command that temporarily changes the setting `set print elements` to 10, then launches the command that follows the second separator `--`. The third part `print` is the command the `pp10` alias will launch, using the temporary values of the settings and the arguments explicitly given by the user. For more information about the `with` command usage, see [Command Settings](Command-Settings.html#Command-Settings).

> 这定义了别名`pp10`为一系列3个命令。第一部分`with print pretty --`暂时激活设置`set print pretty`，然后启动分隔符`--`后面的命令。紧接着第一部分的命令也是一个`with`命令，暂时改变设置`set print elements`为10，然后启动第二个分隔符`--`后面的命令。第三部分`print`是`pp10`别名将启动的命令，使用设置的临时值和用户明确给出的参数。有关`with`命令使用的更多信息，请参见[命令设置](Command-Settings.html#Command-Settings)。


By default, asking the help for an alias shows the documentation of the aliased command. When the alias is a set of nested commands, `help` of an alias shows the documentation of the first command. This help is not particularly useful for an alias such as `pp10`. For such an alias, it is useful to give a specific documentation using the `document` command (see [document](Define.html#Define)).

> 默认情况下，请求别名的帮助会显示别名命令的文档。当别名是一组嵌套命令时，别名的`help`会显示第一个命令的文档。对于像`pp10`这样的别名，这种帮助不是特别有用。对于这样的别名，使用`document`命令提供特定的文档是有用的（参见[document](Define.html#Define))。

::: footnote

---

#### Footnotes

### [(18)](#DOCF18)


[GDB] could easily accept default arguments for pre-defined commands and aliases, but it was deemed this would be confusing, and so is not allowed.

> GDB可以轻松地接受预定义命令和别名的默认参数，但被认为这会令人困惑，因此不允许。
:::

---

::: header

Up: [Aliases](Aliases.html#Aliases)]

> 上：[别名](Aliases.html#Aliases)
:::
