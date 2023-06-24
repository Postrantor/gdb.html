---
tip: translate by openai@2023-06-24 01:40:18
...
---
description: Python Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Python Commands (Debugging with GDB)
lang: en
resource-type: document
title: Python Commands (Debugging with GDB)
---
::: header
Next: [Python API](Python-API.html#Python-API)]
:::

---

#### 23.3.1 Python Commands


[GDB] provides two commands for accessing the Python interpreter, and one related setting:

> [GDB]提供了两个用于访问Python解释器的命令和一个相关设置：

`python-interactive [command]`

`pi [command]`


Without an argument, the `python-interactive` command can be used to start an interactive Python prompt. To return to [GDB] on an empty prompt).

> 没有参数时，可以使用`python-interactive`命令启动交互式Python提示符。 要在空提示符上返回[GDB])。


Alternatively, a single-line Python command can be given as an argument and evaluated. If the command is an expression, the result will be printed; otherwise, nothing will be printed. For example:

> 另外，可以将单行Python命令作为参数传递并进行求值。如果命令是表达式，则会打印结果；否则，不会打印任何内容。例如：

::: smallexample

```bash
(gdb) python-interactive 2 + 3
5
```

:::

`python [command]`

`py [command]`

The `python` command can be used to evaluate Python code.


If given an argument, the `python` command will evaluate the argument as a Python command. For example:

> 如果给出一个参数，`python`命令会将参数作为Python命令进行评估。例如：

::: smallexample

```bash
(gdb) python print 23
23
```

:::


If you do not provide an argument to `python`, it will act as a multi-line command, like `define`. In this case, the Python script is made up of subsequent command lines, given after the `python` command. This command list is terminated using a line containing `end`. For example:

> 如果你没有为`python`提供参数，它将充当多行命令，就像`define`一样。在这种情况下，Python脚本由在`python`命令之后给出的后续命令行组成。使用包含`end`的行来终止此命令列表。例如：

::: smallexample

```bash
(gdb) python
>print 23
>end
23
```

:::

`set python print-stack`


By default, [GDB] will print only the message component of a Python exception when an error occurs in a Python script. This can be controlled using `set python print-stack`: if `full`, then full Python stack printing is enabled; if `none`, then Python stack and message printing is disabled; if `message`, the default, only the message component of the error is printed.

> 默认情况下，当Python脚本中发生错误时，GDB只会打印Python异常的消息部分。可以使用`set python print-stack`来控制：如果是`full`，则启用完整的Python堆栈输出；如果是`none`，则禁用Python堆栈和消息输出；如果是`message`，则默认只打印错误消息部分。

`set python ignore-environment [on|off]`

By default this option is '`off`.


If this option is set to '`on`'s startup process, then this option must be placed into the early initialization file (see [Initialization Files](Initialization-Files.html#Initialization-Files)) to have the desired effect.

> 如果将此选项设置为“启动过程”，则必须将此选项放入早期初始化文件（参见[初始化文件] (Initialization-Files.html#Initialization-Files))以获得所需的效果。


This option is equivalent to passing `-E` to the real `python` executable.

> 这个选项相当于在真正的 `python` 可执行文件中传递 `-E` 选项。

`set python dont-write-bytecode [auto|on|off]`

When this option is '`off` files.


If this option is set to '`on`'s startup process, then this option must be placed into the early initialization file (see [Initialization Files](Initialization-Files.html#Initialization-Files)) to have the desired effect.

> 如果将此选项设置为“启动过程”，则必须将此选项放入早期初始化文件（参见[初始化文件]（Initialization-Files.html#Initialization-Files））以获得所需的效果。


By default this option is set to '`auto`', the environment variable `PYTHONDONTWRITEBYTECODE` is examined to see if it should write out byte-code or not. `PYTHONDONTWRITEBYTECODE` is considered to be off/disabled either when set to the empty string or when the environment variable doesn't exist. All other settings, including those which don't seem to make sense, indicate that it's on/enabled.

> 默认情况下，此选项设置为“auto”，将检查环境变量`PYTHONDONTWRITEBYTECODE`以查看是否应输出字节码。当设置为空字符串或不存在环境变量时，`PYTHONDONTWRITEBYTECODE`被认为是关闭/禁用的。所有其他设置，包括那些似乎没有意义的设置，都表明它是打开/启用的。


This option is equivalent to passing `-B` to the real `python` executable.

> 这个选项相当于给真正的`python`可执行文件传递`-B`参数。


It is also possible to execute a Python script from the [GDB] interpreter:

> 可以在GDB解释器中执行Python脚本。

`source script-name`


:   The script name must end with '`.py` must be configured to recognize the script language based on filename extension using the `script-extension` setting. See [Extending GDB](Extending-GDB.html#Extending-GDB).

> 脚本名称必须以“.py”结尾，必须使用“script-extension”设置来识别基于文件名扩展名的脚本语言。请参阅[扩展GDB](Extending-GDB.html#Extending-GDB)。

The following commands are intended to help debug [GDB] itself:

`set debug py-breakpoint on|off`

`show debug py-breakpoint`

When '`on`' by default.

`set debug py-unwind on|off`

`show debug py-unwind`

When '`on`' by default.

::: footnote

---

#### Footnotes

### [(19)](#DOCF19)


See the ENVIRONMENT VARIABLES section of `man 1 python` for a comprehensive list.

> 查看 `man 1 python` 中的环境变量部分，获取全面的列表。
:::

---

::: header
Next: [Python API](Python-API.html#Python-API)]
:::
