---
tip: translate by openai@2023-06-24 00:20:20
...
---
description: Messages/Warnings (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Messages/Warnings (Debugging with GDB)
lang: en
resource-type: document
title: Messages/Warnings (Debugging with GDB)
---
::: header
Next: [Debugging Output](Debugging-Output.html#Debugging-Output)]
:::

---

### 22.9 Optional Warnings and Messages


By default, [GDB] tell you when it does a lengthy internal operation, so you will not think it has crashed.

> 默认情况下，GDB会在进行较长的内部操作时通知您，这样您就不会认为它已经崩溃了。


Currently, the messages controlled by `set verbose` are those which announce that the symbol table for a source file is being read; see `symbol-file` in [Commands to Specify Files](Files.html#Files).

> 目前，由`set verbose`控制的消息是宣布正在读取源文件的符号表的消息；请参阅[指定文件的命令](Files.html#Files)中的`symbol-file`。

`set verbose on`

Enables [GDB] output of certain informational messages.

`set verbose off`

Disables [GDB] output of certain informational messages.

`show verbose`

Displays whether `set verbose` is on or off.


By default, if [GDB] encounters bugs in the symbol table of an object file, it is silent; but if you are debugging a compiler, you may find this information useful (see [Errors Reading Symbol Files](Symbol-Errors.html#Symbol-Errors)).

> 默认情况下，如果GDB在对象文件的符号表中遇到错误，它会保持沉默；但是，如果您正在调试编译器，您可能会发现这些信息有用（请参见[读取符号文件错误](Symbol-Errors.html#Symbol-Errors)）。

`set complaints limit`


Permits [GDB] to zero to suppress all complaints; set it to a large number to prevent complaints from being suppressed.

> 允许[GDB]将值设为零以抑制所有投诉；将其设置为一个较大的数字以防止投诉被压制。

`show complaints`

Displays how many symbol complaints [GDB] is permitted to produce.


By default, [GDB] is cautious, and asks what sometimes seems to be a lot of stupid questions to confirm certain commands. For example, if you try to run a program which is already running:

> 默认情况下，GDB会谨慎行事，并且会询问有时看起来很多愚蠢的问题来确认某些命令。例如，如果你试图运行一个已经在运行的程序：

::: smallexample

```bash
(gdb) run
The program being debugged has been started already.
Start it from the beginning? (y or n)
```

:::


If you are willing to unflinchingly face the consequences of your own commands, you can disable this "feature":

> 如果你愿意毫不畏缩地面对自己命令的后果，你可以禁用这个“功能”：

`set confirm off`


Disables confirmation requests. Note that running [GDB] option (see [-batch](Mode-Options.html#Mode-Options)) also automatically disables confirmation requests.

> 禁用确认请求。请注意，运行[GDB]选项（参见[-batch](Mode-Options.html#Mode-Options)）也会自动禁用确认请求。

`set confirm on`

Enables confirmation requests (the default).

`show confirm`

Displays state of confirmation requests.


If you need to debug user-defined commands or sourced files you may find it useful to enable *command tracing*. In this mode each command will be printed as it is executed, prefixed with one or more '`+`' symbols, the quantity denoting the call depth of each command.

> 如果您需要调试用户定义的命令或源文件，您可能会发现启用*命令跟踪*很有用。 在此模式下，每个命令都将在执行时以一个或多个“+”符号前缀打印，其数量表示每个命令的调用深度。

`set trace-commands on`

Enable command tracing.

`set trace-commands off`

Disable command tracing.

`show trace-commands`

Display the current state of command tracing.

---

::: header
Next: [Debugging Output](Debugging-Output.html#Debugging-Output)]
:::
