---
tip: translate by openai@2023-06-23 19:16:06
...
---
description: Commands In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Commands In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Commands In Guile (Debugging with GDB)
---
::: header
Next: [Parameters In Guile](Parameters-In-Guile.html#Parameters-In-Guile)]
:::

---

#### 23.4.3.11 Commands In Guile

You can implement new [GDB] from `make-command`.


There is no support for multi-line commands, that is commands that consist of multiple lines and are terminated with `end`.

> 不支持多行命令，也就是由多行组成并以`end`结束的命令。

*


:   The argument `name` consists of multiple words, then the initial words are looked for as prefix commands. In this case, if one of the prefix commands does not exist, an exception is raised.

> 参数`name`由多个单词组成，那么会先查找前缀命令。在这种情况下，如果其中一个前缀命令不存在，则会引发异常。

```
The result is the `<gdb:command>` object representing the command. The command is not usable until it has been registered with [GDB] with `register-command!`.

The rest of the arguments are optional.

The argument `invoke` `error` call. Otherwise, the return value is ignored.

The argument `command-class` how to categorize the new command in the help system. The default is `COMMAND_NONE`.

The argument `completer` how to perform completion for this command. If not provided or if the value is `#f`, then no completion is performed on the command.

The argument `prefix` is a boolean flag indicating whether the new command is a prefix command; sub-commands of this command may be registered.

The argument `doc-string` is help text for the new command. If no documentation string is provided, the default value "This command is not documented." is used.
```

```
<!-- -->
```

Scheme Procedure: **register-command!** *command*


:   Add `command`'s list of commands. It is an error to register a command more than once. The result is unspecified.

> 添加`command`的命令列表。注册一个命令多次是错误的。结果是不确定的。

```
<!-- -->
```

Scheme Procedure: **command?** *object*


:   Return `#t` if `object` is a `<gdb:command>` object. Otherwise return `#f`.

> 如果对象是<gdb:command>对象，则返回#t，否则返回#f。

Scheme Procedure: **dont-repeat**


:   By default, a [GDB] command is repeated when the user enters a blank line at the command prompt. A command can suppress this behavior by invoking the `dont-repeat` function. This is similar to the user command `dont-repeat`, see [dont-repeat](Define.html#Define).

> 默认情况下，当用户在命令提示符下输入空行时，[GDB] 命令会重复。命令可以通过调用`dont-repeat`函数来禁止此行为。这与用户命令`dont-repeat`类似，请参见[dont-repeat](Define.html#Define)。

```
<!-- -->
```

Scheme Procedure: **string-\>argv** *string*


:   Convert a string to a list of strings split up according to [GDB]'s argv parsing rules. It is recommended to use this for consistency. Arguments are separated by spaces and may be quoted. Example:

> 将字符串按照[GDB]的argv解析规则转换为字符串列表。建议使用此功能以获得一致性。参数用空格分隔，可以引用。例子：

```
::: smallexample
``` smallexample
scheme@(guile-user)> (string->argv "1 2\\ \\\"3 '4 \"5' \"6 '7\"")
$1 = ("1" "2 \"3" "4 \"5" "6 '7")
```

:::

```

```

<!-- -->

```

Scheme Procedure: **throw-user-error** *message . args*

:   Throw a `gdb:user-error` exception. The argument `message`.

```

This is used when the command detects a user error of some kind, say a bad command argument.

::: smallexample

```bash
(gdb) guile (use-modules (gdb))
(gdb) guile
(register-command! (make-command "test-user-error"
  #:command-class COMMAND_OBSCURE
  #:invoke (lambda (self arg from-tty)
    (throw-user-error "Bad argument ~a" arg))))
end
(gdb) test-user-error ugh
ERROR: Bad argument ugh
```

:::

```



completer: **self** *text word*


:   If the `completer` holds the last word of the command line; this is computed using a word-breaking heuristic.

> 如果`完成程序`保存了命令行的最后一个单词，则使用词法分析启发式算法来计算。

```

All forms of completion are handled by this function, that is, the TAB and M-? key bindings (see [Completion](Completion.html#Completion)), and the `complete` command (see [complete](Help.html#Help)).

This procedure can return several kinds of values:

- If the return value is a list, the contents of the list are used as the completions. It is up to `completer` to ensure that the contents actually do complete the word. An empty list is allowed, it means that there were no completions available. Only string elements of the list are used; other elements in the list are ignored.
- If the return value is a `<gdb:iterator>` object, it is iterated over to obtain the completions. It is up to `completer-procedure` to ensure that the results actually do complete the word. Only string elements of the result are used; other elements in the sequence are ignored.
- All other results are treated as though there were no available completions.

```


When a new command is registered, it will have been declared as a member of some general class of commands. This is used to classify top-level commands in the on-line help system; note that prefix commands are not listed under their own category but rather that of their top-level command. The available classifications are represented by constants defined in the `gdb` module:

> 当注册一个新的命令时，它将被声明为一般命令类别的成员。这用于在在线帮助系统中对顶级命令进行分类；请注意，前缀命令不会列在自己的类别下，而是列在其顶级命令的类别下。可用的分类由`gdb`模块中定义的常量表示：

`COMMAND_NONE` 


:   The command does not belong to any particular class. A command in this category will not be displayed in any of the help categories. This is the default.

> 这个命令不属于任何特定类别。这类命令不会在任何帮助类别中显示。这是默认设置。

`COMMAND_RUNNING` 


:   The command is related to running the inferior. For example, `start`, `step`, and `continue` are in this category. Type [help running] prompt to see a list of commands in this category.

> 命令与运行次级程序有关。例如，`start`，`step`和`continue`属于此类别。输入[help running]提示以查看此类别中的命令列表。

`COMMAND_DATA` 


:   The command is related to data or variables. For example, `call`, `find`, and `print` are in this category. Type [help data] prompt to see a list of commands in this category.

> 这个命令与数据或变量有关。例如，`call`、`find`和`print`都属于这一类。输入[help data]提示来查看此类命令的列表。

`COMMAND_STACK` 


:   The command has to do with manipulation of the stack. For example, `backtrace`, `frame`, and `return` are in this category. Type [help stack] prompt to see a list of commands in this category.

> 命令与堆栈操作有关。例如，`backtrace`、`frame`和`return`都属于此类别。输入[help stack]提示以查看此类别中的命令列表。

`COMMAND_FILES` 


:   This class is used for file-related commands. For example, `file`, `list` and `section` are in this category. Type [help files] prompt to see a list of commands in this category.

> 这个类用于文件相关的命令。例如，`file`，`list`和`section`都属于这一类。输入[help files]提示以查看这一类别中的命令列表。

`COMMAND_SUPPORT` 


:   This should be used for "support facilities", generally meaning things that are useful to the user when interacting with [GDB] prompt to see a list of commands in this category.

> 这应该用于“支持设施”，一般指在与[GDB]提示交互时对用户有用的东西。查看此类别中的命令列表。

`COMMAND_STATUS` 


:   The command is an '`info` prompt to see a list of commands in this category.

> 命令是一个'`info`提示，以查看此类别中的命令列表。

`COMMAND_BREAKPOINTS` 


:   The command has to do with breakpoints. For example, `break`, `clear`, and `delete` are in this category. Type [help breakpoints] prompt to see a list of commands in this category.

> 命令与断点有关。例如，`break`，`clear`和`delete`都属于此类。输入[help breakpoints]提示以查看此类别中的命令列表。

`COMMAND_TRACEPOINTS` 


:   The command has to do with tracepoints. For example, `trace`, `actions`, and `tfind` are in this category. Type [help tracepoints] prompt to see a list of commands in this category.

> 命令与跟踪点有关。例如，`trace`，`actions`和`tfind`都属于此类别。输入[help tracepoints]提示以查看此类别中的命令列表。

`COMMAND_USER` 


:   The command is a general purpose command for the user, and typically does not fit in one of the other categories. Type [help user-defined] prompt to see a list of commands in this category, as well as the list of gdb macros (see [Sequences](Sequences.html#Sequences)).

> 命令是一般用户的通用命令，通常不属于其他类别之一。输入[帮助用户定义]提示以查看此类别中的命令列表，以及GDB宏的列表（参见[序列](Sequences.html#Sequences)）。

`COMMAND_OBSCURE` 


:   The command is only used in unusual circumstances, or is not of general interest to users. For example, `checkpoint`, `fork`, and `stop` are in this category. Type [help obscure] prompt to see a list of commands in this category.

> 这个命令只在异常情况下使用，或者不是用户的一般兴趣。例如，'checkpoint'，'fork'和'stop'都属于这一类。输入[help obscure]提示以查看此类别中的命令列表。

`COMMAND_MAINTENANCE` 


:   The command is only useful to [GDB] prompt to see a list of commands in this category.

> 命令只对[GDB]提示有用，以查看该类别中的命令列表。


A new command can use a predefined completion function, either by specifying it via an argument at initialization, or by returning it from the `completer` procedure. These predefined completion constants are all defined in the `gdb` module:

> 一个新的命令可以使用一个预定义的完成函数，要么在初始化时通过一个参数指定，要么从`completer`过程中返回。这些预定义的完成常量都定义在`gdb`模块中：

`COMPLETE_NONE` 

:   This constant means that no completion should be done.

`COMPLETE_FILENAME` 

:   This constant means that filename completion should be performed.

`COMPLETE_LOCATION` 


:   This constant means that location completion should be done. See [Location Specifications](Location-Specifications.html#Location-Specifications).

> 这个常量意味着应该完成位置完成。请参阅[位置规范](Location-Specifications.html#Location-Specifications)。

`COMPLETE_COMMAND` 


:   This constant means that completion should examine [GDB] command names.

> 这个常量意味着完成应该检查[GDB]命令名称。

`COMPLETE_SYMBOL` 


:   This constant means that completion should be done using symbol names as the source.

> 这个常量意味着应该使用符号名称作为源来完成。

`COMPLETE_EXPRESSION` 


:   This constant means that completion should be done on expressions. Often this means completing on symbol names, but some language parsers also have support for completing on field names.

> 这个常量意味着完成应该完成在表达式上。通常这意味着完成符号名称，但是一些语言解析器也支持完成字段名称。


The following code snippet shows how a trivial CLI command can be implemented in Guile:

> 以下代码片段展示了如何在Guile中实现一个简单的CLI命令：

::: smallexample

```bash
(gdb) guile
(register-command! (make-command "hello-world"
  #:command-class COMMAND_USER
  #:doc "Greet the whole world."
  #:invoke (lambda (self args from-tty) (display "Hello, World!\n"))))
end
(gdb) hello-world
Hello, World!
```

:::

---

::: header
Next: [Parameters In Guile](Parameters-In-Guile.html#Parameters-In-Guile)]
:::
