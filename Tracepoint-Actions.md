---
tip: translate by openai@2023-06-24 04:08:05
...
---
description: Tracepoint Actions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Tracepoint Actions (Debugging with GDB)
lang: en
resource-type: document
title: Tracepoint Actions (Debugging with GDB)
---
::: header
Next: [Listing Tracepoints](Listing-Tracepoints.html#Listing-Tracepoints)]
:::

---

#### 13.1.6 Tracepoint Action Lists

`actions [num]`


This command will prompt for a list of actions to be taken when the tracepoint is hit. If the tracepoint number `num` is not specified, this command sets the actions for the one that was most recently defined (so that you can define a tracepoint and then say `actions` without bothering about its number). You specify the actions themselves on the following lines, one action at a time, and terminate the actions list with a line containing just `end`. So far, the only defined actions are `collect`, `teval`, and `while-stepping`.

> 此命令将提示一个动作列表，以便在触发断点时执行。如果未指定断点编号`num`，则此命令将为最近定义的断点设置动作（因此，您可以定义断点，然后说“动作”而不必担心其编号）。您在接下来的行中指定动作本身，一次一个动作，并用只包含`end`的行终止动作列表。到目前为止，唯一定义的动作是`collect`、`teval`和`while-stepping`。

`actions` is actually equivalent to `commands` (see [Breakpoint Command Lists](Break-Commands.html#Break-Commands)), except that only the defined actions are allowed; any other [GDB] command is rejected.

To remove all actions from a tracepoint, type '`actions num`'.

::: smallexample

```bash
(gdb) collect data // collect some data

(gdb) while-stepping 5 // single-step 5 times, collect data

(gdb) end              // signals the end of actions.
```

:::


In the following example, the action list begins with `collect` commands indicating the things to be collected when the tracepoint is hit. Then, in order to single-step and collect additional data following the tracepoint, a `while-stepping` command is used, followed by the list of things to be collected after each step in a sequence of single steps. The `while-stepping` command is terminated by its own separate `end` command. Lastly, the action list is terminated by an `end` command.

> 在下面的例子中，操作列表以`collect`命令开头，表示在触发跟踪点时要收集的东西。然后，为了在跟踪点后单步执行并收集额外的数据，使用`while-stepping`命令，后面跟着在一系列单步中每一步要收集的东西的列表。`while-stepping`命令由其自己的`end`命令终止。最后，操作列表由一个`end`命令终止。

::: smallexample

```bash
(gdb) trace foo
(gdb) actions
Enter actions for tracepoint 1, one per line:
> collect bar,baz
> collect $regs
> while-stepping 12
  > collect $pc, arr[i]
  > end
end
```

:::

`collect[/mods] expr1, expr2, …`


Collect values of the given expressions when the tracepoint is hit. This command accepts a comma-separated list of any valid expressions. In addition to global, static, or local variables, the following special arguments are supported:

> 收集给定表达式的值，当跟踪点被命中时。此命令接受任何有效表达式的逗号分隔列表。除了全局、静态或局部变量外，还支持以下特殊参数：

`$regs`

:   Collect all registers.

`$args`

:   Collect all function arguments.

`$locals`

:   Collect all local variables.

`$_ret`


:   Collect the return address. This is helpful if you want to see more of a backtrace.

> 收集返回地址。如果你想看到更多的回溯，这将会很有帮助。

```
*Note:* The return address location can not always be reliably determined up front, and the wrong address / registers may end up collected instead. On some architectures the reliability is higher for tracepoints at function entry, while on others it's the opposite. When this happens, backtracing will stop because the return address is found unavailable (unless another collect rule happened to match it).
```

`$_probe_argc`


:   Collects the number of arguments from the static probe at which the tracepoint is located. See [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points).

> 收集从静态探针处所在的跟踪点的参数数量。参见[静态探针点](Static-Probe-Points.html#Static-Probe-Points)。

`$_probe_argn`


:   `n` th argument from the static probe at which the tracepoint is located. See [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points).

> 第n个静态探针位置的参数。请参阅[静态探针点](Static-Probe-Points.html#Static-Probe-Points)。

`$_sdata`

:

```
Collect static tracepoint marker specific data. Only available for static tracepoints. See [Tracepoint Action Lists](#Tracepoint-Actions). On the UST static tracepoints library backend, an instrumentation point resembles a `printf` function call. The tracing library is able to collect user specified data formatted to a character string using the format provided by the programmer that instrumented the program. Other backends have similar mechanisms. Here's an example of a UST marker call:

::: smallexample
``` smallexample
 const char master_name = "$your_name";
 trace_mark(channel1, marker1, "hello %s", master_name)
```

:::

In this case, collecting `$_sdata` collects the string '`hello $yourname`.

```


You can give several consecutive `collect` commands, each one with a single argument, or one `collect` command with several arguments separated by commas; the effect is the same.

> 你可以连续给出几个`collect`命令，每个命令只有一个参数，或者可以给出一个`collect`命令，用逗号分隔的多个参数；效果是一样的。

The optional `mods`'.


The command `info scope` (see [info scope](Symbols.html#Symbols)) is particularly useful for figuring out what data to collect.

> 命令`info scope`（参见[info scope](Symbols.html#Symbols)）特别有用，可以帮助您确定要收集哪些数据。



`teval expr1, expr2, …`


Evaluate the given expressions when the tracepoint is hit. This command accepts a comma-separated list of expressions. The results are discarded, so this is mainly useful for assigning values to trace state variables (see [Trace State Variables](Trace-State-Variables.html#Trace-State-Variables)) without adding those values to the trace buffer, as would be the case if the `collect` action were used.

> 评估当跟踪点被触发时给定的表达式。此命令接受逗号分隔的表达式列表。结果将被丢弃，因此这主要用于将值分配给跟踪状态变量（参见[跟踪状态变量]（Trace-State-Variables.html#Trace-State-Variables））而不像使用`collect`操作那样将这些值添加到跟踪缓冲区中。



`while-stepping n`


Perform `n` single-step instruction traces after the tracepoint, collecting new data after each step. The `while-stepping` command is followed by the list of what to collect while stepping (followed by its own `end` command):

> 在跟踪点之后，执行n条单步指令跟踪，每步收集新的数据。while-stepping命令之后是要收集的内容的列表（后跟自己的end命令）：

::: smallexample

```bash
> while-stepping 12
  > collect $regs, myglobal
  > end
>
```

:::


Note that `$pc` is not automatically collected by `while-stepping`; you need to explicitly collect that register if you need it. You may abbreviate `while-stepping` as `ws` or `stepping`.

> 注意，`$pc`不会自动由`while-stepping`收集；如果您需要，您需要明确收集该寄存器。您可以将`while-stepping`缩写为`ws`或`stepping`。

`set default-collect expr1, expr2, …`


This variable is a list of expressions to collect at each tracepoint hit. It is effectively an additional `collect` action prepended to every tracepoint action list. The expressions are parsed individually for each tracepoint, so for instance a variable named `xyz` may be interpreted as a global for one tracepoint, and a local for another, as appropriate to the tracepoint's location.

> 这个变量是一个在每次跟踪点命中时收集的表达式列表。它实际上是附加到每个跟踪点操作列表之前的一个“收集”操作。这些表达式将针对每个跟踪点单独解析，因此，例如，一个名为“xyz”的变量可以根据跟踪点的位置分别解释为全局或局部变量。

`show default-collect`


Show the list of expressions that are collected by default at each tracepoint hit.

> 在每次跟踪点命中时默认收集的表达式列表。

---

::: header
Next: [Listing Tracepoints](Listing-Tracepoints.html#Listing-Tracepoints)]
:::
