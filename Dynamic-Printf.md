---
tip: translate by openai@2023-06-23 20:44:34
...
---
description: Dynamic Printf (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Dynamic Printf (Debugging with GDB)
lang: en
resource-type: document
title: Dynamic Printf (Debugging with GDB)
---
::: header
Next: [Save Breakpoints](Save-Breakpoints.html#Save-Breakpoints)]
:::

---

#### 5.1.8 Dynamic Printf


The dynamic printf command `dprintf` combines a breakpoint with formatted printing of your program's data to give you the effect of inserting `printf` calls into your program on-the-fly, without having to recompile it.

> 命令`dprintf`的动态`printf`结合了断点和格式化的程序数据打印，让你可以实时地插入`printf`调用，而无需重新编译程序。


In its most basic form, the output goes to the GDB console. However, you can set the variable `dprintf-style` for alternate handling. For instance, you can ask to format the output by calling your program's `printf` function. This has the advantage that the characters go to the program's output device, so they can recorded in redirects to files and so forth.

> 在最基本的形式中，输出会发送到GDB控制台。但是，您可以设置变量`dprintf-style`以处理其他操作。例如，您可以通过调用程序的`printf`函数来请求格式化输出。这具有优势，即字符会发送到程序的输出设备，因此可以将它们记录在重定向到文件等中。


If you are doing remote debugging with a stub or agent, you can also ask to have the printf handled by the remote agent. In addition to ensuring that the output goes to the remote program's device along with any other output the program might produce, you can also ask that the dprintf remain active even after disconnecting from the remote target. Using the stub/agent is also more efficient, as it can do everything without needing to communicate with [GDB].

> 如果您正在使用存根或代理进行远程调试，您还可以要求由远程代理处理printf。除了确保输出转到远程程序的设备以及程序可能产生的任何其他输出之外，您还可以要求dprintf在断开与远程目标的连接后仍然保持活动状态。使用存根/代理也更有效，因为它可以在无需与[GDB]通信的情况下完成所有操作。

`dprintf locspec,template,expression[,expression…]`


Whenever execution reaches a code location that results from resolving `locspec`. To print several values, separate them with commas.

> 每当执行到从解析`locspec`而来的代码位置时，要打印几个值，请用逗号隔开。

`set dprintf-style style`


Set the dprintf output to be handled in one of several different styles enumerated below. A change of style affects all existing dynamic printfs immediately. (If you need individual control over the print commands, simply define normal breakpoints with explicitly-supplied command lists.)

> 将dprintf输出设置为按下面列出的多种不同样式处理。样式的改变会立即影响所有现有的动态打印。（如果需要对打印命令进行单独控制，可以使用提供明确命令列表的常规断点。）

`gdb`

:

```
Handle the output using the [GDB]' format specifier (see [%V Format Specifier](Output.html#g_t_0025V-Format-Specifier)).
```

`call`

:

```
Handle the output by calling a function in your program (normally `printf`). When using this style the supported format specifiers depend entirely on the function being called.

Most of [GDB]' style dprintf, care should be taken to ensure that only format specifiers supported by the output function are used, otherwise the results will be undefined.
```

`agent`

:

```
Have the remote debugging agent (such as `gdbserver`) handle the output itself. This style is only available for agents that support running commands on the target. This style does not support the '`%V`' format specifier.
```

`set dprintf-function function`


Set the function to call if the dprintf style is `call`. By default its value is `printf`. You may set it to any expression that [GDB] can evaluate to a function, as per the `call` command.

> 将函数设置为如果dprintf样式为`call`时调用。默认值为`printf`。您可以将其设置为[GDB]可以评估为函数的任何表达式，如`call`命令所述。

`set dprintf-channel channel`


Set a "channel" for dprintf. If set to a non-empty value, [GDB] will evaluate it as an expression and pass the result as a first argument to the `dprintf-function`, in the manner of `fprintf` and similar functions. Otherwise, the dprintf format string will be the first argument, in the manner of `printf`.

> 设置一个"通道"给dprintf。如果设置为非空值，[GDB]将会把它作为表达式进行求值，并将结果作为第一个参数传递给`dprintf-function`，就像`fprintf`和类似的函数一样。否则，dprintf格式字符串将作为第一个参数，就像`printf`一样。


As an example, if you wanted `dprintf` output to go to a logfile that is a standard I/O stream assigned to the variable `mylog`, you could do the following:

> 例如，如果您想要将`dprintf`输出发送到分配给变量`mylog`的标准I/O流中的日志文件，可以执行以下操作：

::: example

```example
(gdb) set dprintf-style call
(gdb) set dprintf-function fprintf
(gdb) set dprintf-channel mylog
(gdb) dprintf 25,"at line 25, glob=%d\n",glob
Dprintf 1 at 0x123456: file main.c, line 25.
(gdb) info break
1       dprintf        keep y   0x00123456 in main at main.c:25
        call (void) fprintf (mylog,"at line 25, glob=%d\n",glob)
        continue
(gdb)
```

:::


Note that the `info break` displays the dynamic printf commands as normal breakpoint commands; you can thus easily see the effect of the variable settings.

> 注意，`info break`会将动态printf命令显示为普通断点命令；因此您可以轻松查看变量设置的效果。

`set disconnected-dprintf on`

`set disconnected-dprintf off`


Choose whether `dprintf` commands should continue to run if [GDB] has disconnected from the target. This only applies if the `dprintf-style` is `agent`.

> 選擇dprintf命令是否應該繼續運行，如果GDB已經與目標斷開連接。這只適用於dprintf風格為agent的情況。

`show disconnected-dprintf off`

Show the current choice for disconnected `dprintf`.

[GDB] will report an error.

---

::: header
Next: [Save Breakpoints](Save-Breakpoints.html#Save-Breakpoints)]
:::
