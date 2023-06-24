---
tip: translate by openai@2023-06-23 18:56:30
...
---
description: CLI Commands In Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: CLI Commands In Python (Debugging with GDB)
lang: en
resource-type: document
title: CLI Commands In Python (Debugging with GDB)
---
::: header
Next: [GDB/MI Commands In Python](GDB_002fMI-Commands-In-Python.html#GDB_002fMI-Commands-In-Python)]
:::

---

#### 23.3.2.20 CLI Commands In Python


You can implement new [GDB] CLI commands in Python. A CLI command is implemented using an instance of the `gdb.Command` class, most commonly using a subclass.

> 你可以用Python来实现新的GDB CLI命令。CLI命令使用gdb.Command类的实例来实现，通常使用子类。

)*


:   The object initializer for `Command` registers the new command with [GDB]. This initializer is normally invoked from the subclass' own `__init__` method.

> `Command` 的对象初始化程序会在 [GDB] 中注册新的命令。这个初始化程序通常是从子类的 `__init__` 方法中调用的。

```
`name` consists of multiple words, then the initial words are looked for as prefix commands. In this case, if one of the prefix commands does not exist, an exception is raised.

There is no support for multi-line commands.

`command_class` how to categorize the new command in the help system.

`completer_class` will attempt to complete using the object's `complete` method (see below); if no such method is found, an error will occur when completion is attempted.

`prefix` is an optional argument. If `True`, then the new command is a prefix command; sub-commands of this command may be registered.

The help text for the new command is taken from the Python documentation string for the command's class, if there is one. If no documentation string is provided, the default value "This command is not documented." is used.
```


Function: **Command.dont_repeat** *()*

> 功能：**Command.dont_repeat**（）


:   By default, a [GDB] command is repeated when the user enters a blank line at the command prompt. A command can suppress this behavior by invoking the `dont_repeat` method at some point in its `invoke` method (normally this is done early in case of exception). This is similar to the user command `dont-repeat`, see [dont-repeat](Define.html#Define).

> 默认情况下，当用户在命令提示符下输入空行时，[GDB] 命令会被重复执行。 命令可以通过在其`invoke`方法中的某个点调用`dont_repeat`方法来禁止此行为（通常在发生异常时会尽早这样做）。 这类似于用户命令`dont-repeat`，请参阅[dont-repeat](Define.html#Define)。

```
<!-- -->
```


Function: **Command.invoke** *(argument, from_tty)*

> 功能：**Command.invoke** *（参数，from_tty）*


:   This method is called by [GDB] when this command is invoked.

> 这个方法被[GDB]调用，当这个命令被调用时。

```
`argument` is a string. It is the argument to the command, after leading and trailing whitespace has been stripped.

`from_tty` is a boolean argument. When true, this means that the command was entered by the user at the terminal; when false it means that the command came from elsewhere.

If this method throws an exception, it is turned into a [GDB] `error` call. Otherwise, the return value is ignored.



To break `argument`'s internal argument lexer `buildargv`. It is recommended to use this for consistency. Arguments are separated by spaces and may be quoted. Example:

::: smallexample
``` smallexample

print gdb.string_to_argv ("1 2\ \\\"3 '4 \"5' \"6 '7\"")

> 打印gdb.string_to_argv("1 2\ \\\"3 '4 \"5' \"6 '7\"")

['1', '2 "3', '4 "5', "6 '7"]

> ['1', '2 "3', '4 "5', "6 '7"]

['1', '2 "3', '4 "5', "6 '7"]
```

:::

```




Function: **Command.complete** *(text, word)*

> 功能：**Command.complete** *（文本，单词）*


:   This method is called by [GDB] when the user attempts completion on this command. All forms of completion are handled by this method, that is, the TAB and M-? key bindings (see [Completion](Completion.html#Completion)), and the `complete` command (see [complete](Help.html#Help)).

> 这种方法被称为[GDB]，当用户尝试在此命令上完成时调用。所有形式的完成都由此方法处理，即TAB和M-?键绑定（参见[完成](Completion.html#Completion)）以及`complete`命令（参见[complete](Help.html#Help)）。

```

The arguments `text` holds the last word of the command line; this is computed using a word-breaking heuristic.

The `complete` method can return several values:

- If the return value is a sequence, the contents of the sequence are used as the completions. It is up to `complete` to ensure that the contents actually do complete the word. A zero-length sequence is allowed, it means that there were no completions available. Only string elements of the sequence are used; other elements in the sequence are ignored.
- If the return value is one of the '`COMPLETE_`-internal completion function is invoked, and its result is used.
- All other results are treated as though there were no available completions.

```


When a new command is registered, it must be declared as a member of some general class of commands. This is used to classify top-level commands in the on-line help system; note that prefix commands are not listed under their own category but rather that of their top-level command. The available classifications are represented by constants defined in the `gdb` module:

> 当注册一个新的命令时，必须将其声明为某个命令的一般类别的成员。这用于在在线帮助系统中对顶级命令进行分类; 请注意，前缀命令不会根据其自身的类别列出，而是根据它们的顶级命令列出。可用的分类由`gdb`模块中定义的常量表示:



`gdb.COMMAND_NONE`


The command does not belong to any particular class. A command in this category will not be displayed in any of the help categories.

> 这个命令不属于任何特定的类别。属于这个类别的命令不会在任何帮助类别中显示。



`gdb.COMMAND_RUNNING`


The command is related to running the inferior. For example, `start`, `step`, and `continue` are in this category. Type [help running] prompt to see a list of commands in this category.

> 这个命令与运行次级程序有关，例如`start`、`step`和`continue`都属于这一类。输入[help running]提示以查看此类命令的列表。



`gdb.COMMAND_DATA`


The command is related to data or variables. For example, `call`, `find`, and `print` are in this category. Type [help data] prompt to see a list of commands in this category.

> 命令与数据或变量有关。例如，`call`，`find`和`print`属于此类别。输入[help data]提示以查看此类别中的命令列表。



`gdb.COMMAND_STACK`


The command has to do with manipulation of the stack. For example, `backtrace`, `frame`, and `return` are in this category. Type [help stack] prompt to see a list of commands in this category.

> 这个命令与堆栈操作有关。例如，`backtrace`，`frame`和`return`都属于这一类。输入[help stack]命令可以查看这一类命令的列表。



`gdb.COMMAND_FILES`


This class is used for file-related commands. For example, `file`, `list` and `section` are in this category. Type [help files] prompt to see a list of commands in this category.

> 这个类用于文件相关的命令。例如，`file`，`list`和`section`都属于这一类。输入[help files]提示，可以查看此类别中的命令列表。



`gdb.COMMAND_SUPPORT`


This should be used for "support facilities", generally meaning things that are useful to the user when interacting with [GDB] prompt to see a list of commands in this category.

> 这应该用于“支持设施”，一般指在与[GDB]提示交互时对用户有用的东西。查看此类别中的命令列表。



`gdb.COMMAND_STATUS`


The command is an '`info` prompt to see a list of commands in this category.

> 命令是一个'info'提示，可以查看此类别中的命令列表。



`gdb.COMMAND_BREAKPOINTS`


The command has to do with breakpoints. For example, `break`, `clear`, and `delete` are in this category. Type [help breakpoints] prompt to see a list of commands in this category.

> 这个命令与断点有关。例如，`break`、`clear`和`delete`都属于这一类。输入[help breakpoints]提示可以查看此类命令的列表。



`gdb.COMMAND_TRACEPOINTS`


The command has to do with tracepoints. For example, `trace`, `actions`, and `tfind` are in this category. Type [help tracepoints] prompt to see a list of commands in this category.

> 这个命令与跟踪点有关。例如，`trace`，`actions`和`tfind`都属于这一类。输入[help tracepoints]提示可以查看这一类命令的列表。



`gdb.COMMAND_TUI`


The command has to do with the text user interface (see [TUI](TUI.html#TUI)). Type [help tui] prompt to see a list of commands in this category.

> 命令与文本用户界面有关（参见[TUI](TUI.html#TUI)）。输入[help tui]提示以查看此类别中的命令列表。



`gdb.COMMAND_USER`


The command is a general purpose command for the user, and typically does not fit in one of the other categories. Type [help user-defined] prompt to see a list of commands in this category, as well as the list of gdb macros (see [Sequences](Sequences.html#Sequences)).

> 命令是用户的通用命令，通常不属于其他类别之一。输入[help user-defined]提示以查看此类别中的命令列表，以及GDB宏列表（参见[序列](Sequences.html#Sequences)）。



`gdb.COMMAND_OBSCURE`


The command is only used in unusual circumstances, or is not of general interest to users. For example, `checkpoint`, `fork`, and `stop` are in this category. Type [help obscure] prompt to see a list of commands in this category.

> 命令只在不寻常的情况下使用，或者对用户来说不是一般感兴趣的。例如，“检查点”，“分叉”和“停止”都属于这一类。输入[help obscure]提示以查看此类命令的列表。



`gdb.COMMAND_MAINTENANCE`


The command is only useful to [GDB] prompt to see a list of commands in this category.

> 命令只对[GDB]提示有用，以查看此类别中的命令列表。


A new command can use a predefined completion function, either by specifying it via an argument at initialization, or by returning it from the `complete` method. These predefined completion constants are all defined in the `gdb` module:

> 一个新的命令可以使用预定义的完成函数，要么通过在初始化时指定它，要么通过从`complete`方法返回它。这些预定义的完成常量都定义在`gdb`模块中：



`gdb.COMPLETE_NONE` 


This constant means that no completion should be done.

> 这个常量意味着不应该完成任何完成工作。



`gdb.COMPLETE_FILENAME` 


This constant means that filename completion should be performed.

> 这个常量意味着应该执行文件名完成。



`gdb.COMPLETE_LOCATION` 


This constant means that location completion should be done. See [Location Specifications](Location-Specifications.html#Location-Specifications).

> 这个常量意味着应该完成位置定位。请参阅[位置规范](Location-Specifications.html#Location-Specifications)。



`gdb.COMPLETE_COMMAND` 


This constant means that completion should examine [GDB] command names.

> 这个常量意味着完成应该检查[GDB]命令名称。



`gdb.COMPLETE_SYMBOL` 


This constant means that completion should be done using symbol names as the source.

> 这个常量意味着应该使用符号名称作为源来完成。



`gdb.COMPLETE_EXPRESSION` 


This constant means that completion should be done on expressions. Often this means completing on symbol names, but some language parsers also have support for completing on field names.

> 这个常量意味着完成应该在表达式上完成。通常这意味着在符号名称上完成，但是一些语言解析器也支持在字段名上完成。


The following code snippet shows how a trivial CLI command can be implemented in Python:

> 下面的代码片段展示了如何在Python中实现一个简单的CLI命令：

::: smallexample

```bash
class HelloWorld (gdb.Command):
  """Greet the whole world."""

  def __init__ (self):
    super (HelloWorld, self).__init__ ("hello-world", gdb.COMMAND_USER)

  def invoke (self, arg, from_tty):
    print ("Hello, World!")

HelloWorld ()
```

:::


The last line instantiates the class, and is necessary to trigger the registration of the command with [GDB], you may need to import the `gdb` module explicitly.

> 最后一行实例化类，并且必须触发与[GDB]的命令注册，你可能需要显式导入`gdb`模块。

---

::: header
Next: [GDB/MI Commands In Python](GDB_002fMI-Commands-In-Python.html#GDB_002fMI-Commands-In-Python)]
:::
