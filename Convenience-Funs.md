---
tip: translate by openai@2023-06-23 19:46:43
...
---
description: Convenience Funs (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Convenience Funs (Debugging with GDB)
lang: en
resource-type: document
title: Convenience Funs (Debugging with GDB)
---
::: header
Next: [Registers](Registers.html#Registers)]
:::

---

### 10.13 Convenience Functions

[GDB].


These functions do not require [GDB] to be configured with `Python` support, which means that they are always available.

> 这些函数不需要GDB配置Python支持，这意味着它们总是可用的。

`$_isvoid (expr)`

Return one if the expression `expr` is `void`. Otherwise it returns zero.


A `void` expression is an expression where the type of the result is `void`. For example, you can examine a convenience variable (see [Convenience Variables](Convenience-Vars.html#Convenience-Vars)) to check whether it is `void`:

> 一个`void`表达式是其结果类型为`void`的表达式。例如，您可以检查一个便利变量（参见[便利变量]（Convenience-Vars.html#Convenience-Vars））来检查它是否为`void`：

::: smallexample

```bash
(gdb) print $_exitcode
$1 = void
(gdb) print $_isvoid ($_exitcode)
$2 = 1
(gdb) run
Starting program: ./a.out
[Inferior 1 (process 29572) exited normally]
(gdb) print $_exitcode
$3 = 0
(gdb) print $_isvoid ($_exitcode)
$4 = 0
```

:::


In the example above, we used `$_isvoid` to check whether `$_exitcode` is `void` before and after the execution of the program being debugged. Before the execution there is no exit code to be examined, therefore `$_exitcode` is `void`. After the execution the program being debugged returned zero, therefore `$_exitcode` is zero, which means that it is not `void` anymore.

> 在上面的例子中，我们使用`$_isvoid`来检查在调试程序执行之前和之后`$_exitcode`是否为`void`。在执行之前没有退出代码可以检查，因此`$_exitcode`是`void`的。在执行之后，被调试的程序返回了零，因此`$_exitcode`是零，这意味着它不再是`void`了。


The `void` expression can also be a call of a function from the program being debugged. For example, given the following function:

> 该`void`表达式也可以是正在调试的程序中的函数调用。例如，给定以下函数：

::: smallexample

```bash
void
foo (void)
{
}
```

:::

The result of calling it inside [GDB] is `void`:

::: smallexample

```bash
(gdb) print foo ()
$1 = void
(gdb) print $_isvoid (foo ())
$2 = 1
(gdb) set $v = foo ()
(gdb) print $v
$3 = void
(gdb) print $_isvoid ($v)
$4 = 1
```

:::

`$_gdb_setting_str (setting)`


Return the value of the [GDB] is any setting that can be used in a `set` or `show` command (see [Controlling GDB](Controlling-GDB.html#Controlling-GDB)).

> 返回[GDB]的值是可以在`set`或`show`命令中使用的任何设置（参见[控制GDB](Controlling-GDB.html#Controlling-GDB)）。

::: smallexample

```bash
(gdb) show print frame-arguments
Printing of non-scalar frame arguments is "scalars".
(gdb) p $_gdb_setting_str("print frame-arguments")
$1 = "scalars"
(gdb) p $_gdb_setting_str("height")
$2 = "30"
(gdb)
```

:::

`$_gdb_setting (setting)`


Return the value of the [GDB]. The type of the returned value depends on the setting.

> 返回[GDB]的值。返回值的类型取决于设定。


The value type for boolean and auto boolean settings is `int`. The boolean values `off` and `on` are converted to the integer values `0` and `1`. The value `auto` is converted to the value `-1`.

> 布尔和自动布尔设置的值类型是`int`。布尔值`off`和`on`被转换为整数值`0`和`1`。值`auto`被转换为值`-1`。


The value type for integer settings is either `unsigned int` or `int`, depending on the setting.

> 整数设置的值类型取决于设置，可以是无符号整数或整数。


Some integer settings accept an `unlimited` value. Depending on the setting, the `set` command also accepts the value `0` or the value `-1` as a synonym for `unlimited`. For example, `set height unlimited` is equivalent to `set height 0`.

> 一些整数设置接受`无限`值。根据设置，`set`命令也接受值`0`或值`-1`作为`无限`的同义词。例如，`set height unlimited`等同于`set height 0`。


Some other settings that accept the `unlimited` value use the value `0` to literally mean zero. For example, `set history size 0` indicates to not record any [GDB] commands in the command history. For such settings, `-1` is the synonym for `unlimited`.

> 对于接受`unlimited`值的其他设置，使用值`0`来表示零。例如，`set history size 0`表示不记录[GDB]命令历史记录。对于这样的设置，`-1`是`unlimited`的同义词。


See the documentation of the corresponding `set` command for the numerical value equivalent to `unlimited`.

> 請參閱對應的`set`命令的文檔，以獲得與`unlimited`相等的數值。


The `$_gdb_setting` function converts the unlimited value to a `0` or a `-1` value according to what the `set` command uses.

> `$_gdb_setting` 功能根据 `set` 命令使用的情况，将无限值转换为 `0` 或 `-1` 的值。

::: smallexample

```bash
(gdb) p $_gdb_setting_str("height")
$1 = "30"
(gdb) p $_gdb_setting("height")
$2 = 30
(gdb) set height unlimited
(gdb) p $_gdb_setting_str("height")
$3 = "unlimited"
(gdb) p $_gdb_setting("height")
$4 = 0
```

```bash
(gdb) p $_gdb_setting_str("history size")
$5 = "unlimited"
(gdb) p $_gdb_setting("history size")
$6 = -1
(gdb) p $_gdb_setting_str("disassemble-next-line")
$7 = "auto"
(gdb) p $_gdb_setting("disassemble-next-line")
$8 = -1
(gdb)
```

:::


Other setting types (enum, filename, optional filename, string, string noescape) are returned as string values.

> 其他设置类型（枚举、文件名、可选文件名、字符串、字符串无转义）将作为字符串值返回。

`$_gdb_maint_setting_str (setting)`


Like the `$_gdb_setting_str` function, but works with `maintenance set` variables.

> 就像`$_gdb_setting_str`函数一样，但是可以使用`maintenance set`变量。

`$_gdb_maint_setting (setting)`


Like the `$_gdb_setting` function, but works with `maintenance set` variables.

> 就像`$_gdb_setting`函数一样，但可以与`maintenance set`变量一起使用。

`$_shell (command-string)`


Invoke a shell to execute `command-string` is a host signal number, not a target signal number. If you're native debugging, they will be the same, but if cross debugging, the host vs target signal numbers may be completely unrelated. Please consult your host operating system's documentation for the mapping between host signal numbers and signal names. The shell to run is determined in the same way as for the `shell` command. See [Shell Commands](Shell-Commands.html#Shell-Commands).

> 调用一个shell来执行`command-string`是一个主机信号编号，而不是一个目标信号编号。如果您是本机调试，它们将是相同的，但如果跨调试，主机和目标信号编号可能完全不相关。请参考您的主机操作系统的文档，了解主机信号编号和信号名称之间的映射关系。要运行的shell将以与`shell`命令相同的方式确定。请参见[Shell Commands](Shell-Commands.html#Shell-Commands)。

::: smallexample

```bash
(gdb) print $_shell("true")
$1 = 0
(gdb) print $_shell("false")
$2 = 1
(gdb) p $_shell("echo hello")
hello
$3 = 0
(gdb) p $_shell("foobar")
bash: line 1: foobar: command not found
$4 = 127
```

:::

This may also be useful in breakpoint conditions. For example:

::: smallexample

```bash
(gdb) break function if $_shell("some command") == 0
```

:::


In this scenario, you'll want to make sure that the shell command you run in the breakpoint condition takes the least amount of time possible. For example, avoid running a command that may block indefinitely, or that sleeps for a while before exiting. Prefer a command or script which analyzes some state and exits immediately. This is important because the debugged program stops for the breakpoint every time, and then [GDB] evaluates the breakpoint condition. If the condition is false, the program is re-resumed transparently, without informing you of the stop. A quick shell command thus avoids significantly slowing down the debugged program unnecessarily.

> 在这种情况下，您希望确保在断点条件中运行的shell命令所花费的时间尽可能少。例如，避免运行可能无限期阻塞或在退出前睡眠一段时间的命令。宁可选择一个可以分析某些状态并立即退出的命令或脚本。这一点很重要，因为被调试的程序每次都会因断点而停止，然后[GDB]会评估断点条件。如果条件为假，程序将被透明地重新恢复，而您不会收到任何通知。因此，快速的shell命令可以避免不必要地显著减慢被调试的程序。


Note: unlike the `shell` command, the `$_shell` convenience function does not affect the `$_shell_exitcode` and `$_shell_exitsignal` convenience variables.

> 注意：与`shell`命令不同，`$_shell`便利函数不会影响`$_shell_exitcode`和`$_shell_exitsignal`便利变量。


The following functions require [GDB] to be configured with `Python` support.

> 以下功能需要GDB配置有Python支持。

`$_memeq(buf1, buf2, length)`

Returns one if the `length` are equal. Otherwise it returns zero.

`$_regex(str, regex)`


Returns one if the string `str`. Otherwise it returns zero. The syntax of the regular expression is that specified by `Python`'s regular expression support.

> 如果字符串`str`存在，则返回1。否则返回0。正则表达式的语法是由Python的正则表达式支持指定的。

`$_streq(str1, str2)`

Returns one if the strings `str1` are equal. Otherwise it returns zero.

`$_strlen(str)`

Returns the length of string `str`.

`$_caller_is(name[, number_of_frames])`


Returns one if the calling function's name is equal to `name`. Otherwise it returns zero.

> 如果调用函数的名称等于`name`，则返回1，否则返回0。


If the optional argument `number_of_frames` is provided, it is the number of frames up in the stack to look. The default is 1.

> 如果提供可选参数`number_of_frames`，则它是要查看堆栈中的帧数。默认值为1。

Example:

::: smallexample

```bash
(gdb) backtrace
#0  bottom_func ()
    at testsuite/gdb.python/py-caller-is.c:21
#1  0x00000000004005a0 in middle_func ()
    at testsuite/gdb.python/py-caller-is.c:27
#2  0x00000000004005ab in top_func ()
    at testsuite/gdb.python/py-caller-is.c:33
#3  0x00000000004005b6 in main ()
    at testsuite/gdb.python/py-caller-is.c:39
(gdb) print $_caller_is ("middle_func")
$1 = 1
(gdb) print $_caller_is ("top_func", 2)
$1 = 1
```

:::

`$_caller_matches(regexp[, number_of_frames])`


Returns one if the calling function's name matches the regular expression `regexp`. Otherwise it returns zero.

> 如果调用函数的名称与正则表达式`regexp`匹配，则返回1。否则返回0。


If the optional argument `number_of_frames` is provided, it is the number of frames up in the stack to look. The default is 1.

> 如果提供了可选参数`number_of_frames`，它是查看堆栈中的帧数。默认值为1。

`$_any_caller_is(name[, number_of_frames])`


Returns one if any calling function's name is equal to `name`. Otherwise it returns zero.

> 如果任何调用函数的名称等于`name`，则返回1。否则返回0。


If the optional argument `number_of_frames` is provided, it is the number of frames up in the stack to look. The default is 1.

> 如果提供了可选参数`number_of_frames`，则它是查看堆栈中的帧数。默认值为1。


This function differs from `$_caller_is` in that this function checks all stack frames from the immediate caller to the frame specified by `number_of_frames`.

> 这个函数与`$_caller_is`的不同之处在于，它检查从直接调用者到由`number_of_frames`指定的帧的所有堆栈帧。

`$_any_caller_matches(regexp[, number_of_frames])`


Returns one if any calling function's name matches the regular expression `regexp`. Otherwise it returns zero.

> 如果任何调用函数的名称与正则表达式`regexp`匹配，则返回1。否则返回0。


If the optional argument `number_of_frames` is provided, it is the number of frames up in the stack to look. The default is 1.

> 如果提供可选参数`number_of_frames`，它将是查找堆栈中的帧数。默认值为1。


This function differs from `$_caller_matches` in that this function checks all stack frames from the immediate caller to the frame specified by `number_of_frames`.

> 这个函数与`$_caller_matches`的不同之处在于，这个函数检查从直接调用者到由`number_of_frames`指定的帧的所有堆栈帧。

`$_as_string(value)`


This convenience function is considered deprecated, and could be removed from future versions of [GDB]' format specifier instead (see [%V Format Specifier](Output.html#g_t_0025V-Format-Specifier)).

> 这个便利函数被认为是过时的，可能会从未来版本的GDB中删除，请使用格式说明符（参见[%V 格式说明符](Output.html#g_t_0025V-Format-Specifier))代替。

Return the string representation of `value`.


This function is useful to obtain the textual label (enumerator) of an enumeration value. For example, assuming the variable `node` is of an enumerated type:

> 这个功能有助于获取枚举值的文本标签（枚举器）。例如，假设变量`node`是枚举类型：

::: smallexample

```bash
(gdb) printf "Visiting node of type %s\n", $_as_string(node)
Visiting node of type NODE_INTEGER
```

:::

`$_cimag(value)`

`$_creal(value)`


Return the imaginary (`$_cimag`) or real (`$_creal`) part of the complex number `value`.

> 返回复数value的虚数（$_cimag）或实数（$_creal）部分。


The type of the imaginary or real part depends on the type of the complex number, e.g., using `$_cimag` on a `float complex` will return an imaginary part of type `float`.

> 类型的虚数或实数部分取决于复数的类型，例如，使用`$_cimag`在`float complex`上将返回一个类型为`float`的虚数部分。

[GDB] provides the ability to list and get help on convenience functions.

`help function`

:

```
Print a list of all convenience functions.
```

---

::: header
Next: [Registers](Registers.html#Registers)]
:::
