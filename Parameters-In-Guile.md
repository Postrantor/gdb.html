---
tip: translate by openai@2023-06-24 01:01:17
...
---
description: Parameters In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Parameters In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Parameters In Guile (Debugging with GDB)
---
::: header
Next: [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile)]
:::

---

#### 23.4.3.12 Parameters In Guile

You can implement new [GDB].


There are many parameters that already exist and can be set in [GDB]. Similarly, you can define parameters that can be used to influence behavior in custom Guile scripts and commands.

> 在[GDB]中已经存在许多可以设置的参数。同样，您也可以定义参数，用于影响自定义Guile脚本和命令的行为。


A new parameter is defined with the `make-parameter` Guile function, and added to [GDB] from `make-parameter`.

> 使用`make-parameter` Guile函数定义一个新参数，并从`make-parameter`添加到[GDB]。


Parameters are exposed to the user via the `set` and `show` commands. See [Help](Help.html#Help).

> 参数可以通过`set`和`show`命令向用户公开。请参阅[帮助](Help.html#Help)。

*


:   The argument `name` consists of multiple words, and no prefix parameter group can be found, an exception is raised.

> 参数`name`包含多个单词，没有找到前缀参数组，抛出异常。

```
The result is the `<gdb:parameter>` object representing the parameter. The parameter is not usable until it has been registered with [GDB] with `register-parameter!`.

The rest of the arguments are optional.

The argument `command-class` how to categorize the new parameter in the help system. The default is `COMMAND_NONE`.

The argument `parameter-type` the type of the new parameter; this information is used for input validation and completion. The default is `PARAM_BOOLEAN`.

If `parameter-type` must be a list of strings. These strings represent the possible values for the parameter.

If `parameter-type` will cause an exception to be thrown.

The argument `set-func`'. A non-empty string result should typically be used for displaying warnings and errors.

The argument `show-func` will add a trailing newline.

The argument `doc` is the help text for the new parameter. If there is no documentation string, a default value is used.

The argument `set-doc` is the help text for this parameter's `set` command.

The argument `show-doc` is the help text for this parameter's `show` command.

The argument `initial-value` specifies the initial value of the parameter. If it is a function, it takes one parameter, the `<gdb:parameter>` object and its result is used as the initial value of the parameter. The initial value must be valid for the parameter type, otherwise an exception is thrown.
```

```
<!-- -->
```

Scheme Procedure: **register-parameter!** *parameter*


:   Add `parameter`'s list of parameters. It is an error to register a parameter more than once. The result is unspecified.

> 添加`参数`的参数列表。注册一个参数多次是错误的。结果是不确定的。

```
<!-- -->
```

Scheme Procedure: **parameter?** *object*


:   Return `#t` if `object` is a `<gdb:parameter>` object. Otherwise return `#f`.

> 如果对象是<gdb:parameter>对象，则返回#t，否则返回#f。

```
<!-- -->
```

Scheme Procedure: **parameter-value** *parameter*


:   Return the value of `parameter` which may either be a `<gdb:parameter>` object or a string naming the parameter.

> 返回`参数`的值，可能是`<gdb:parameter>`对象或指定参数的字符串。

```
<!-- -->
```

Scheme Procedure: **set-parameter-value!** *parameter new-value*

:   Assign `parameter` does validation when assignments are made.


When a new parameter is defined, its type must be specified. The available types are represented by constants defined in the `gdb` module:

> 当定义一个新参数时，必须指定它的类型。可用类型由`gdb`模块中定义的常量表示。

`PARAM_BOOLEAN`


:   The value is a plain boolean. The Guile boolean values, `#t` and `#f` are the only valid values.

> 值是一个普通布尔值。Guile布尔值`#t`和`#f`是唯一有效的值。

`PARAM_AUTO_BOOLEAN`


:   The value has three possible states: true, false, and '`auto`' is represented using `#:auto`.

> 值有三种可能的状态：真，假，以及使用`#:auto`表示的'`auto`'。

`PARAM_UINTEGER`


:   The value is an unsigned integer. The value of `#:unlimited` should be interpreted to mean "unlimited", and the value of '`0`' is reserved and should not be used.

> 值是一个无符号整数。“#：unlimited”的值应被解释为“无限”，而‘0’的值保留不得使用。

`PARAM_ZINTEGER`

:   The value is an integer.

`PARAM_ZUINTEGER`

:   The value is an unsigned integer.

`PARAM_ZUINTEGER_UNLIMITED`


:   The value is an integer in the range '`[0, INT_MAX]`' is reserved and should not be used, and other negative numbers are not allowed.

> 值必须是范围在[0, INT_MAX]之间的整数，其他负数都不允许使用。

`PARAM_STRING`


:   The value is a string. When the user modifies the string, any escape sequences, such as '`\t`', and octal escapes, are translated into corresponding characters and encoded into the current host charset.

> 值是一个字符串。当用户修改字符串时，所有转义序列，如'\t'，八进制转义符，都会被转换成相应的字符，并编码成当前主机字符集。

`PARAM_STRING_NOESCAPE`


:   The value is a string. When the user modifies the string, escapes are passed through untranslated.

> 值是一个字符串。当用户修改字符串时，转义会原样传递。

`PARAM_OPTIONAL_FILENAME`

:   The value is a either a filename (a string), or `#f`.

`PARAM_FILENAME`


:   The value is a filename. This is just like `PARAM_STRING_NOESCAPE`, but uses file names for completion.

> 值是一个文件名。这就像`PARAM_STRING_NOESCAPE`一样，但使用文件名进行完成。

`PARAM_ENUM`


:   The value is a string, which must be one of a collection of string constants provided when the parameter is created.

> 值是一个字符串，必须是在参数创建时提供的字符串常量集合之一。

::: footnote

---

#### Footnotes

### [(20)](#DOCF20)


Note that [GDB] parameters must not be confused with Guileâ€™s parameter objects (see [Parameters](http://www.gnu.org/software/guile/manual/html_node/Parameters.html#Parameters) in GNU Guile Reference Manual).

> 注意，GDB参数不应与Guile的参数对象混淆（参见GNU Guile参考手册中的[参数](http://www.gnu.org/software/guile/manual/html_node/Parameters.html#Parameters)）。
:::

---

::: header
Next: [Progspaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile)]
:::
