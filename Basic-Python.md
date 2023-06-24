---
tip: translate by openai@2023-06-23 17:54:26
...
---
description: Basic Python (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Basic Python (Debugging with GDB)
lang: en
resource-type: document
title: Basic Python (Debugging with GDB)
---
::: header
Next: [Exception Handling](Exception-Handling.html#Exception-Handling)]
:::

---

#### 23.3.2.1 Basic Python


At startup, [GDB]'s output-paging streams. A Python program which outputs to one of these streams may have its output interrupted by the user (see [Screen Size](Screen-Size.html#Screen-Size)). In this situation, a Python `KeyboardInterrupt` exception is thrown.

> 在启动时，[GDB]的输出分页流。一个输出到这些流中的Python程序可能会被用户中断（参见[Screen Size]（Screen-Size.html#Screen-Size））。在这种情况下，Python会抛出`KeyboardInterrupt`异常。


Some care must be taken when writing Python code to run in [GDB]. Two things worth noting in particular:

> 在编写用于[GDB]运行的Python代码时，必须要小心。特别值得注意的两件事：

- [GDB] will most likely stop working correctly. Note that it is unfortunately common for GUI toolkits to install a `SIGCHLD` handler.
- [GDB] takes care to mark its internal file descriptors as close-on-exec. However, this cannot be done in a thread-safe way on all platforms. Your Python programs should be aware of this and should both create new file descriptors with the close-on-exec flag set and arrange to close unneeded file descriptors before starting a child process.


[GDB] automatically `import` s the `gdb` module for use in all scripts evaluated by the `python` command.

> GDB会自动为python命令评估的所有脚本导入gdb模块。


Some types of the `gdb` module come with a textual representation (accessible through the `repr` or `str` functions). These are offered for debugging purposes only, expect them to change over time.

> 一些`gdb`模块带有文本表示(通过`repr`或`str`函数访问)。这些仅用于调试目的，预计它们会随着时间的推移而改变。


Variable: **gdb.PYTHONDIR**

> 变量：**gdb.PYTHONDIR**


:   A string containing the python directory (see [Python](Python.html#Python)).

> 一个包含Python目录的字符串（见[Python](Python.html#Python)）。

)*


:   Evaluate `command` runs, it is translated as described in [Exception Handling](Exception-Handling.html#Exception-Handling).

> 评估`命令`运行，参见[异常处理](Exception-Handling.html#Exception-Handling)中的描述来进行翻译。

```
The `from_tty` ought to consider this command as having originated from the user invoking it interactively. It must be a boolean value. If omitted, it defaults to `False`.

By default, any output produced by `command` virtual terminal will be temporarily set to unlimited width and height, and its pagination will be disabled; see [Screen Size](Screen-Size.html#Screen-Size).
```


Function: **gdb.breakpoints** *()*

> 功能：**gdb.breakpoints** *（）*


:   Return a sequence holding all of [GDB] version 7.11 and earlier, this function returned `None` if there were no breakpoints. This peculiarity was subsequently fixed, and now `gdb.breakpoints` returns an empty sequence in this case.

> 返回一个包含所有[GDB]版本7.11及更早版本的序列，如果没有断点，此函数将返回“无”。随后修复了这种特性，现在`gdb.breakpoints`在这种情况下返回一个空序列。

```
<!-- -->
```

)*


:   Return a Python list holding a collection of newly set `gdb.Breakpoint` objects matching function names defined by the `regex` keyword takes a Python iterable that yields a collection of `gdb.Symtab` objects and will restrict the search to those functions only contained within the `gdb.Symtab` objects.

> 返回一个Python列表，其中包含一组新设置的`gdb.Breakpoint`对象，这些对象匹配由`regex`关键字定义的函数名，该关键字接受一个Python可迭代对象，该对象会产生一组`gdb.Symtab`对象，并将搜索限制为仅包含在`gdb.Symtab`对象中的函数。


Function: **gdb.parameter** *(parameter)*

> 函数：**gdb.parameter**（参数）


:   Return the value of a [GDB]' is a valid parameter name.

> 返回[GDB]的值是一个有效的参数名称。

```
If the named parameter does not exist, this function throws a `gdb.error` (see [Exception Handling](Exception-Handling.html#Exception-Handling)). Otherwise, the parameter's value is converted to a Python value of the appropriate type, and returned.
```


Function: **gdb.set_parameter** *(name, value)*

> 函数：**gdb.set_parameter**（名称，值）


:   Sets the gdb parameter `name`. As with `gdb.parameter`, the parameter name string may contain spaces if the parameter has a multi-part name.

> 设置gdb参数`name`。与`gdb.parameter`一样，如果参数名称具有多个部分，参数名称字符串可以包含空格。


Function: **gdb.with_parameter** *(name, value)*

> 功能：gdb.with_parameter（名称，值）


:   Create a Python context manager (for use with the Python `with` statement) that temporarily sets the gdb parameter `name`. On exit from the context, the previous value will be restored.

> 创建一个Python上下文管理器（用于Python的`with`语句），用于暂时设置gdb参数`name`。在退出上下文时，将恢复先前的值。

```
This uses `gdb.parameter` in its implementation, so it can throw the same exceptions as that function.

For example, it's sometimes useful to evaluate some Python code with a particular gdb language:

::: smallexample
``` smallexample

with gdb.with_parameter('language', 'pascal'):

> 使用gdb.with_parameter('language', 'pascal')：

  ... language-specific operations

> ...语言特定的操作
```

:::

```




Function: **gdb.history** *(number)*

> 功能：**gdb.history** *（数字）*


:   Return a value from [GDB] doesn't exist in the value history, a `gdb.error` exception will be raised.

> 如果从[GDB]中返回的值不存在于值历史记录中，将会引发一个`gdb.error`异常。

```

If no exception is raised, the return value is always an instance of `gdb.Value` (see [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)).

```

```

<!-- -->

```


Function: **gdb.add_history** *(value)*

> 功能：**gdb.add_history**（值）


:   Takes `value` can't be converted to a `gdb.Value` then a `TypeError` is raised.

> 如果将值无法转换为gdb.Value，则会引发TypeError。

```

When a command implemented in Python prints a single `gdb.Value` as its result, then placing the value into the history will allow the user convenient access to those values via CLI history facilities.

```

```

<!-- -->

```


Function: **gdb.history_count** *()*

> 功能：**gdb.history_count** *（）*


:   Return an integer indicating the number of values in [GDB]'s value history (see [Value History](Value-History.html#Value-History)).

> 返回一个整数，表示[GDB]的值历史中的值数量（参见[值历史](Value-History.html#Value-History)）。




Function: **gdb.convenience_variable** *(name)*

> 函数：**gdb.convenience_variable** *（名称）*


:   Return the value of the convenience variable (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) named `name`' that is used to mark a convenience variable in an expression. If the convenience variable does not exist, then `None` is returned.

> 返回方便变量（参见[Convenience Vars](Convenience-Vars.html#Convenience-Vars)）中名为`name`的值。如果方便变量不存在，则返回`None`。




Function: **gdb.set_convenience_variable** *(name, value)*

> 函数：**gdb.set_convenience_variable** *（名称，值）*


:   Set the value of the convenience variable (see [Convenience Vars](Convenience-Vars.html#Convenience-Vars)) named `name` is not a `gdb.Value` (see [Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)), it is is converted using the `gdb.Value` constructor.

> 设置方便变量（参见[Convenience Vars](Convenience-Vars.html#Convenience-Vars))命名为`name`的值不是`gdb.Value`（参见[Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)），它是使用`gdb.Value`构造函数转换而来的。



)*


:   Parse `expression`, which must be a string, as an expression in the current language, evaluate it, and return the result as a `gdb.Value`.

> 解析`表达式`，它必须是一个字符串，作为当前语言中的表达式进行评估，并将结果作为`gdb.Value`返回。

```

`global_context`', meaning that the current frame or current static context should be used.

This function can be useful when implementing a new command (see [CLI Commands In Python](CLI-Commands-In-Python.html#CLI-Commands-In-Python), see [GDB/MI Commands In Python](GDB_002fMI-Commands-In-Python.html#GDB_002fMI-Commands-In-Python)), as it provides a way to parse the command's argument as an expression. It is also useful simply to compute values.

```




Function: **gdb.find_pc_line** *(pc)*

> 功能：**gdb.find_pc_line**（pc）


:   Return the `gdb.Symtab_and_line` object corresponding to the `pc` is passed as an argument, then the `symtab` and `line` attributes of the returned `gdb.Symtab_and_line` object will be `None` and 0 respectively. This is identical to `gdb.current_progspace().find_pc_line(pc)` and is included for historical compatibility.

> 返回作为参数传递的`pc`对应的`gdb.Symtab_and_line`对象，然后返回的`gdb.Symtab_and_line`对象的`symtab`和`line`属性将分别为`None`和0。这与`gdb.current_progspace().find_pc_line(pc)`是完全相同的，仅仅是为了兼容历史。




Function: **gdb.post_event** *(event)*

> 功能：**gdb.post_event** *（事件）*

:   Put `event`.

```

[GDB] thread. `post_event` ensures this. For example:

::: smallexample

```bash
(gdb) python
>import threading
>
>class Writer():
> def __init__(self, message):
>        self.message = message;
> def __call__(self):
>        gdb.write(self.message)
>
>class MyThread1 (threading.Thread):
> def run (self):
>        gdb.post_event(Writer("Hello "))
>
>class MyThread2 (threading.Thread):
> def run (self):
>        gdb.post_event(Writer("World\n"))
>
>MyThread1().start()
>MyThread2().start()
>end
(gdb) Hello World
```

:::

```



)*


:   Print a string to [GDB]'s standard output stream. Possible stream values are:

> 打印一个字符串到GDB的标准输出流。可能的流值有：

:   

`gdb.STDOUT`


:   [GDB]'s standard output stream.

> GDB的标准输出流。

```

```

`gdb.STDERR`


:   [GDB]'s standard error stream.

> GDB的标准错误流。

```

```

`gdb.STDLOG`


:   [GDB]'s log stream (see [Logging Output](Logging-Output.html#Logging-Output)).

> GDB 的日志流（参见[日志输出](Logging-Output.html#Logging-Output））


Writing to `sys.stdout` or `sys.stderr` will automatically call this function and will automatically direct the output to the relevant stream.

> 写入`sys.stdout`或`sys.stderr`将自动调用此函数，并将输出自动重定向到相关流。



)*


:   Flush the buffer of a [GDB]'s standard output stream. Possible stream values are:

> 清空GDB的标准输出流的缓冲区。可能的流值是：

:   

`gdb.STDOUT`


:   [GDB]'s standard output stream.

> GDB的标准输出流。

```

```

`gdb.STDERR`


:   [GDB]'s standard error stream.

> GDB的标准错误流。

```

```

`gdb.STDLOG`


:   [GDB]'s log stream (see [Logging Output](Logging-Output.html#Logging-Output)).

> 日志流（参见[日志输出](Logging-Output.html#Logging-Output)）（GDB）。


Flushing `sys.stdout` or `sys.stderr` will automatically call this function for the relevant stream.

> 刷新`sys.stdout`或`sys.stderr`将会自动为相关流调用此函数。




Function: **gdb.target_charset** *()*

> 功能：**gdb.target_charset** *（）*


:   Return the name of the current target character set (see [Character Sets](Character-Sets.html#Character-Sets)). This differs from `gdb.parameter('target-charset')` in that '`auto`' is never returned.

> 返回当前目标字符集的名称（参见[字符集](Character-Sets.html#Character-Sets)）。这与`gdb.parameter('target-charset')`的不同之处在于，永远不会返回“自动”。




Function: **gdb.target_wide_charset** *()*

> 功能：**gdb.target_wide_charset***（）*


:   Return the name of the current target wide character set (see [Character Sets](Character-Sets.html#Character-Sets)). This differs from `gdb.parameter('target-wide-charset')` in that '`auto`' is never returned.

> 返回当前目标宽字符集的名称（参见[字符集](Character-Sets.html#Character-Sets)）。这与`gdb.parameter('target-wide-charset')`的不同之处在于'`auto`'永远不会被返回。




Function: **gdb.host_charset** *()*

> 函数：**gdb.host_charset** *（）*


:   Return a string, the name of the current host character set (see [Character Sets](Character-Sets.html#Character-Sets)). This differs from `gdb.parameter('host-charset')` in that '`auto`' is never returned.

> 返回一个字符串，它是当前主机字符集的名称（参见[字符集] (Character-Sets.html#Character-Sets)）。这与`gdb.parameter('host-charset')`的不同之处在于永远不会返回'`auto`'。




Function: **gdb.solib_name** *(address)*

> 功能：**gdb.solib_name** *（地址）*


:   Return the name of the shared library holding the given `address` as a string, or `None`. This is identical to `gdb.current_progspace().solib_name(address)` and is included for historical compatibility.

> 返回包含给定地址的共享库的名称，作为字符串，或者为`None`。这与`gdb.current_progspace().solib_name(address)`完全相同，仅仅是为了历史兼容性而包含。



)*


:   Return locations of the line specified by `expression`'s inbuilt `break` or `edit` commands do (see [Location Specifications](Location-Specifications.html#Location-Specifications)).

> 返回由内置的`break`或`edit`命令指定的行的位置（参见[位置规范](Location-Specifications.html#Location-Specifications)）。

```

<!-- -->

```


Function: **gdb.prompt_hook** *(current_prompt)*

> 功能：**gdb.prompt_hook** *（当前提示）*

:   

```

If `prompt_hook`.

The parameter `current_prompt` contains the current [GDB] will continue to use the current prompt.

Some prompts cannot be substituted in [GDB]. Secondary prompts such as those used by readline for command input, and annotation related prompts are prohibited from being changed.

```




Function: **gdb.architecture_names** *()*

> 功能：**gdb.architecture_names** *（）*


:   Return a list containing all of the architecture names that the current build of [GDB] supports. Each architecture name is a string. The names returned in this list are the same names as are returned from `gdb.Architecture.name` (see [Architecture.name](Architectures-In-Python.html#gdbpy_005farchitecture_005fname)).

> 返回一个包含当前[GDB]构建支持的所有架构名称的列表。每个架构名称都是一个字符串。此列表中返回的名称与从`gdb.Architecture.name`返回的名称相同（请参阅[Architecture.name](Architectures-In-Python.html#gdbpy_005farchitecture_005fname)）。




Function: **gdb.connections**

> 功能：**gdb.connections**


:   Return a list of `gdb.TargetConnection` objects, one for each currently active connection (see [Connections In Python](Connections-In-Python.html#Connections-In-Python)). The connection objects are in no particular order in the returned list.

> 返回一个`gdb.TargetConnection`对象的列表，每个当前活动连接有一个（参见[Python中的连接](Connections-In-Python.html#Connections-In-Python)）。连接对象在返回的列表中没有特定的顺序。

```

<!-- -->

```

)*


:   Return a string in the format '`addr <symbol+offset>` in decimal.

> 返回一个以十进制格式的字符串 'addr <符号 + 偏移量>'。

```

If no suitable `symbol` (see [Print Settings](Print-Settings.html#Print-Settings)).

Additionally, the returned string can include file name and line number information when [set print symbol-filename on]'.

The `progspace`, e.g. in order to determine the size of an address in bytes.

If neither `progspace` will use the program space and architecture of the currently selected inferior, thus, the following two calls are equivalent:

::: smallexample

```bash

gdb.format_address(address)

> gdb.格式化地址（地址）

gdb.format_address(address,

> gdb.格式化地址（地址）
                   gdb.selected_inferior().progspace,
                   gdb.selected_inferior().architecture())
```

:::

It is not valid to only pass one of `progspace`, either they must both be provided, or neither must be provided (and the defaults will be used).

This method uses the same mechanism for formatting address, symbol, and offset information as core [GDB].

Here are some examples of the possible string formats:

::: smallexample

```bash
0x00001042
0x00001042 <symbol+16>

0x00001042 <symbol+16 at file.c:123>

> 0x00001042 <符号+16 在文件.c：123>
```

:::

```

```

<!-- -->

```


Function: **gdb.current_language** *()*

> 功能：**gdb.current_language** *（）*


:   Return the name of the current language as a string. Unlike `gdb.parameter('language')`, this function will never return '`auto`'. If a `gdb.Frame` object is available (see [Frames In Python](Frames-In-Python.html#Frames-In-Python)), the `language` method might be preferable in some cases, as that is not affected by the user's language setting.

> 返回当前语言的名称作为一个字符串。不像`gdb.parameter('language')`，这个函数永远不会返回'`auto`'。如果有`gdb.Frame`对象可用（参见[Python中的帧](Frames-In-Python.html#Frames-In-Python)），在某些情况下，`language`方法可能更可取，因为它不受用户语言设置的影响。

---

::: header
Next: [Exception Handling](Exception-Handling.html#Exception-Handling)]
:::
```
