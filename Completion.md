---
tip: translate by openai@2023-06-23 19:23:24
...
---
description: Completion (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Completion (Debugging with GDB)
lang: en
resource-type: document
title: Completion (Debugging with GDB)
---
::: header
Next: [Command Options](Command-Options.html#Command-Options)]
:::

---

### 3.3 Command Completion


[GDB] subcommands, command options, and the names of symbols in your program.

> [GDB] 子命令、命令选项和程序中的符号名称。


Press the TAB key whenever you want [GDB] fills in the word, and waits for you to finish the command (or press RET to enter it). For example, if you type

> 按下 TAB 键，当你想要 GDB 填充单词时，它会等待你完成命令（或按下 RET 进入）。例如，如果你输入

::: smallexample

```bash
(gdb) info breTAB
```

:::

[GDB]':

::: smallexample

```bash
(gdb) info breakpoints
```

:::


You can either press RET at this point, to run the `info breakpoints` command, or backspace and enter something else, if '`breakpoints`', to exploit command abbreviations rather than command completion).

> 此时你可以按下RET键来运行`info breakpoints`命令，或者按下退格键并输入其他内容（如'`breakpoints`'，以利用命令缩写而不是命令完成）。


If there is more than one possibility for the next word when you press TAB, [GDB] just sounds the bell. Typing TAB again displays all the function names in your program that begin with those characters, for example:

> 如果按下TAB时下一个单词有多个可能性，[GDB]就会发出警报声。再次按下TAB会显示以这些字符开头的程序中的所有函数名，例如：

::: smallexample

```bash
(gdb) b make_TAB
```

```bash
GDB sounds bell; press TAB again, to see:
```

```bash
make_a_section_from_file     make_environ
make_abs_section             make_function_type
make_blockvector             make_pointer_type
make_cleanup                 make_reference_type
make_command                 make_symbol_completion_list
(gdb) b make_
```

:::


After displaying the available possibilities, [GDB]' in the example) so you can finish the command.

> 在显示可用可能性之后，[GDB]


If the command you are trying to complete expects either a keyword or a number to follow, then '`NUMBER`' will be shown among the available completions, for example:

> 如果您要完成的命令需要跟随关键字或数字，那么“NUMBER”将显示在可用的完成项中，例如：“简体中文”

::: smallexample

```bash
(gdb) print -elements TABTAB
NUMBER     unlimited
(gdb) print -elements 
```

:::


Here, the option expects a number (e.g., `100`), not literal `NUMBER`. Such metasyntactical arguments are always presented in uppercase.

> 这里，选项需要一个数字（例如`100`），而不是文字`NUMBER`。这种元语法参数总是用大写字母表示。


If you just want to see the list of alternatives in the first place, you can press [M-?].

> 如果你只想首先看到替代选项的列表，你可以按[M-?]。


If the number of possible completions is large, [GDB] will print as much of the list as it has collected, as well as a message indicating that the list may be truncated.

> 如果可能的完成数量很多，[GDB]会打印出它已经收集的列表，以及指示列表可能已截断的消息。

::: smallexample

```bash
(gdb) b mTABTAB
main
<... the rest of the possible completions ...>
*** List may be truncated, max-completions reached. ***
(gdb) b m
```

:::

This behavior can be controlled with the following commands:

`set max-completions limit`

`set max-completions unlimited`

Set the maximum number of completion candidates. [GDB]

`show max-completions`


Show the maximum number of candidates that [GDB] will collect and show during completion.

> 显示GDB在补全时收集和显示的最大候选数量。


Sometimes the string you need, while logically a "word", may contain parentheses or other characters that [GDB] commands.

> 有时，您需要的字符串，尽管在逻辑上是一个“单词”，可能包含括号或其他[GDB]命令。


A likely situation where you might need this is in typing an expression that involves a C++ symbol name with template parameters. This is because when completing expressions, GDB treats the '`<`' character as word delimiter, assuming that it's the less-than comparison operator (see [C and C++ Operators](C-Operators.html#C-Operators)).

> 可能需要这个的情况是在输入涉及C++符号名称的表达式时。这是因为在完成表达式时，GDB将'<'字符视为单词分隔符，假定它是小于比较运算符（参见[C和C++运算符](C-Operators.html#C-Operators)）。


For example, when you want to call a C++ template function interactively using the `print` or `call` commands, you may need to distinguish whether you mean the version of `name` that was specialized for `int`, `name<int>()`, or the version that was specialized for `float`, `name<float>()`. To use the word-completion facilities in this situation, type a single quote `'` at the beginning of the function name. This alerts [GDB] to request word completion:

> 例如，当您想使用`print`或`call`命令以交互方式调用C ++模板函数时，您可能需要区分是专门为`int`定制的`name`版本`name <int>（）`，还是专门为`float`定制的版本`name <float>（）`。要在此情况下使用单词完成功能，请在函数名称开头输入单引号`'`。这将警告[GDB]要求完成单词：

::: smallexample

```bash
(gdb) p 'func<M-?
func<int>()    func<float>()
(gdb) p 'func<
```

:::


When setting breakpoints however (see [Location Specifications](Location-Specifications.html#Location-Specifications)), you don't usually need to type a quote before the function name, because [GDB] understands that you want to set a breakpoint on a function:

> 当设置断点（参见[位置规范](Location-Specifications.html#Location-Specifications)）时，通常不需要在函数名称前面输入引号，因为[GDB]知道您想在函数上设置断点：

::: smallexample

```bash
(gdb) b func<M-?
func<int>()    func<float>()
(gdb) b func<
```

:::


This is true even in the case of typing the name of C++ overloaded functions (multiple definitions of the same function, distinguished by argument type). For example, when you want to set a breakpoint you don't need to distinguish whether you mean the version of `name` that takes an `int` parameter, `name(int)`, or the version that takes a `float` parameter, `name(float)`.

> 即使在输入C++重载函数的名称（同一函数的多个定义，通过参数类型区分）的情况下也是如此。例如，当您想要设置断点时，您不需要区分您是指带有`int`参数的`name（int）`版本，还是带有`float`参数的`name（float）`版本。

::: smallexample

```bash
(gdb) b bubble(M-?
bubble(int)    bubble(double)
(gdb) b bubble(douM-?
bubble(double)
```

:::


See [quoting names](Symbols.html#quoting-names) for a description of other scenarios that require quoting.

> 请参阅[引用名称](Symbols.html#quoting-names)以了解其他需要引用的场景的描述。


For more information about overloaded functions, see [C++ Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions). You can use the command `set overload-resolution off` to disable overload resolution; see [[GDB] Features for C++](Debugging-C-Plus-Plus.html#Debugging-C-Plus-Plus).

> 有关重载函数的更多信息，请参阅[C++ Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions)。您可以使用命令`set overload-resolution off`禁用重载解析;请参阅[[GDB] Features for C++](Debugging-C-Plus-Plus.html#Debugging-C-Plus-Plus)。


When completing in an expression which looks up a field in a structure, [GDB] to limit completions to the field names available in the type of the left-hand-side:

> 当在表达式中完成查找结构中的字段时，[GDB] 限制完成项为左侧类型可用的字段名称。

::: smallexample

```bash
(gdb) p gdb_stdout.M-?
magic                to_fputs             to_rewind
to_data              to_isatty            to_write
to_delete            to_put               to_write_async_safe
to_flush             to_read
```

:::


This is because the `gdb_stdout` is a variable of the type `struct ui_file` that is defined in [GDB] sources as follows:

> 因为`gdb_stdout`是[GDB]源码中定义的`struct ui_file`类型的变量。

::: smallexample

```bash
struct ui_file
{
   int *magic;
   ui_file_flush_ftype *to_flush;
   ui_file_write_ftype *to_write;
   ui_file_write_async_safe_ftype *to_write_async_safe;
   ui_file_fputs_ftype *to_fputs;
   ui_file_read_ftype *to_read;
   ui_file_delete_ftype *to_delete;
   ui_file_isatty_ftype *to_isatty;
   ui_file_rewind_ftype *to_rewind;
   ui_file_put_ftype *to_put;
   void *to_data;
}
```

:::

::: footnote

---

#### Footnotes

### [(3)](#DOCF3)


The completer can be confused by certain kinds of invalid expressions. Also, it only examines the static type of the expression, not the dynamic type.

> 完成者可能会被某些无效表达式所迷惑。此外，它只检查表达式的静态类型，而不是动态类型。
:::

---

::: header
Next: [Command Options](Command-Options.html#Command-Options)]
:::
