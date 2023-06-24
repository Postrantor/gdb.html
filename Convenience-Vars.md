---
tip: translate by openai@2023-06-23 19:50:07
...
---
description: Convenience Vars (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Convenience Vars (Debugging with GDB)
lang: en
resource-type: document
title: Convenience Vars (Debugging with GDB)
---
::: header
Next: [Convenience Funs](Convenience-Funs.html#Convenience-Funs)]
:::

---

### 10.12 Convenience Variables


[GDB]; they are not part of your program, and setting a convenience variable has no direct effect on further execution of your program. That is why you can use them freely.

> [GDB]：它们不是您的程序的一部分，设置一个方便变量不会直接影响您程序的进一步执行。这就是为什么您可以自由使用它们的原因。


Convenience variables are prefixed with '`$`'. See [Value History](Value-History.html#Value-History).)

> 变量前缀带有'$'。参见[值历史](Value-History.html#Value-History)。


You can save a value in a convenience variable with an assignment expression, just as you would set a variable in your program. For example:

> 你可以使用赋值表达式将一个值保存在一个便利变量中，就像你在程序中设置一个变量一样。例如：

::: smallexample

```bash
set $foo = *object_ptr
```

:::


would save in `$foo` the value contained in the object pointed to by `object_ptr`.

> 將`object_ptr`指向物件中包含的值儲存在`$foo`中。


Using a convenience variable for the first time creates it, but its value is `void` until you assign a new value. You can alter the value with another assignment at any time.

> 使用方便变量第一次创建它时，它的值为`void`，直到您赋予新值。您可以随时通过另一个赋值来更改值。


Convenience variables have no fixed types. You can assign a convenience variable any type of value, including structures and arrays, even if that variable already has a value of a different type. The convenience variable, when used as an expression, has the type of its current value.

> 方便变量没有固定的类型。您可以为方便变量分配任何类型的值，包括结构和数组，即使该变量已具有不同类型的值。当作为表达式使用时，方便变量具有其当前值的类型。

`show convenience`


Print a list of convenience variables used so far, and their values, as well as a list of the convenience functions. Abbreviated `show conv`.

> 打印出已使用的方便变量的列表及其值，以及方便函数的列表。简写为“show conv”。

`init-if-undefined $variable = expression`


Set a convenience variable if it has not already been set. This is useful for user-defined commands that keep some state. It is similar, in concept, to using local static variables with initializers in C (except that convenience variables are global). It can also be used to allow users to override default values used in a command script.

> 如果尚未设置，请设置一个便利变量。这对于保持某些状态的用户定义命令非常有用。在概念上，它类似于在C中使用具有初始值的局部静态变量（除了便利变量是全局的）。它还可以用来允许用户覆盖命令脚本中使用的默认值。


If the variable is already defined then the expression is not evaluated so any side-effects do not occur.

> 如果变量已经定义，那么表达式不会被求值，因此不会发生任何副作用。


One of the ways to use a convenience variable is as a counter to be incremented or a pointer to be advanced. For example, to print a field from successive elements of an array of structures:

> 一种使用方便变量的方法是用作计数器进行递增或指针进行前进。例如，打印数组结构的连续元素的字段：

::: smallexample

```bash
set $i = 0
print bar[$i++]->contents
```

:::

Repeat that command by typing RET.


Some convenience variables are created automatically by [GDB] and given values likely to be useful.

> GDB会自动创建一些便利变量，并赋予可能有用的值。

`$_`


The variable `$_` is automatically set by the `x` command to the last address examined (see [Examining Memory](Memory.html#Memory)). Other commands which provide a default address for `x` to examine also set `$_` to that address; these commands include `info line` and `info breakpoint`. The type of `$_` is `void *` except when set by the `x` command, in which case it is a pointer to the type of `$__`.

> 变量`$_`由`x`命令自动设置为最后检查的地址（参见[检查内存](Memory.html#Memory)）。其他为`x`提供默认地址的命令也会将`$_`设置为该地址；这些命令包括`info line`和`info breakpoint`。除了由`x`命令设置时，`$_`的类型为`void *`，此时它是指向`$__`类型的指针。

`$__`


The variable `$__` is automatically set by the `x` command to the value found in the last address examined. Its type is chosen to match the format in which the data was printed.

> 变量`$__`由`x`命令自动设置为最后检查的地址中找到的值。其类型选择为与数据打印的格式相匹配。

`$_exitcode`


When the program being debugged terminates normally, [GDB] automatically sets this variable to the exit code of the program, and resets `$_exitsignal` to `void`.

> 当被调试的程序正常终止时，[GDB]会自动将此变量设置为程序的退出代码，并将`$_exitsignal`重置为`void`。

`$_exitsignal`


When the program being debugged dies due to an uncaught signal, [GDB] automatically sets this variable to that signal's number, and resets `$_exitcode` to `void`.

> 当调试的程序由于未捕获的信号而死亡时，[GDB]会自动将此变量设置为该信号的编号，并将`$_exitcode`重置为`void`。


To distinguish between whether the program being debugged has exited (i.e., `$_exitcode` is not `void`) or signalled (i.e., `$_exitsignal` is not `void`), the convenience function `$_isvoid` can be used (see [Convenience Functions](Convenience-Funs.html#Convenience-Funs)). For example, considering the following source code:

> 为了区分被调试的程序是否已退出（即`$_exitcode`不是`void`）或者已经发出信号（即`$_exitsignal`不是`void`），可以使用便利函数`$_isvoid`（参见[Convenience Functions](Convenience-Funs.html#Convenience-Funs)）。例如，考虑以下源代码：

::: smallexample

```bash
#include <signal.h>

int
main (int argc, char *argv)
{
  raise (SIGALRM);
  return 0;
}
```

:::


A valid way of telling whether the program being debugged has exited or signalled would be:

> 一种有效的方法来检查被调试的程序是否已经退出或发出信号，就是：

::: smallexample

```bash
(gdb) define has_exited_or_signalled
Type commands for definition of ``has_exited_or_signalled''.
End with a line saying just ``end''.
>if $_isvoid ($_exitsignal)
 >echo The program has exited\n
 >else
 >echo The program has signalled\n
 >end
>end
(gdb) run
Starting program:

Program terminated with signal SIGALRM, Alarm clock.
The program no longer exists.
(gdb) has_exited_or_signalled
The program has signalled
```

:::

As can be seen, [GDB] would report a normal exit:

::: smallexample

```bash
(gdb) has_exited_or_signalled
The program has exited
```

:::

`$_exception`


The variable `$_exception` is set to the exception object being thrown at an exception-related catchpoint. See [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints).

> 变量`$_exception`被设置为在异常相关的捕获点抛出的异常对象。参见[设置捕获点](Set-Catchpoints.html#Set-Catchpoints)。

`$_ada_exception`


The variable `$_ada_exception` is set to the address of the exception being caught or thrown at an Ada exception-related catchpoint. See [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints).

> 变量`$_ada_exception`被设置为捕获或抛出的Ada异常相关捕获点的地址。请参见[设置捕获点](Set-Catchpoints.html#Set-Catchpoints)。

`$_probe_argc`

`$_probe_arg0…$_probe_arg11`


Arguments to a static probe. See [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points).

> 参数到静态探针。参见[静态探针点](Static-Probe-Points.html#Static-Probe-Points)。

`$_sdata`


The variable `$_sdata` contains extra collected static tracepoint data. See [Tracepoint Action Lists](Tracepoint-Actions.html#Tracepoint-Actions). Note that `$_sdata` could be empty, if not inspecting a trace buffer, or if extra static tracepoint data has not been collected.

> 变量`$_sdata`包含额外收集的静态跟踪点数据。请参阅[跟踪点操作列表](Tracepoint-Actions.html#Tracepoint-Actions)。请注意，如果没有检查跟踪缓冲区或没有收集额外的静态跟踪点数据，`$_sdata`可能为空。

`$_siginfo`


The variable `$_siginfo` contains extra signal information (see [extra signal information](Signals.html#extra-signal-information)). Note that `$_siginfo` could be empty, if the application has not yet received any signals. For example, it will be empty before you execute the `run` command.

> 变量`$_siginfo`包含额外的信号信息（请参阅[额外信号信息](Signals.html#extra-signal-information)）。请注意，如果应用程序尚未收到任何信号，`$_siginfo`可能为空。例如，在执行`run`命令之前，它将为空。

`$_tlb`


The variable `$_tlb` is automatically set when debugging applications running on MS-Windows in native mode or connected to gdbserver that supports the `qGetTIBAddr` request. See [General Query Packets](General-Query-Packets.html#General-Query-Packets). This variable contains the address of the thread information block.

> 变量`$_tlb`在调试运行在MS-Windows本机模式或连接到支持`qGetTIBAddr`请求的gdbserver上的应用程序时会自动设置。请参阅[一般查询包](General-Query-Packets.html#General-Query-Packets)。此变量包含线程信息块的地址。

`$_inferior`


The number of the current inferior. See [Debugging Multiple Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs).

> 当前下级的数量。参见[调试多个下级连接和程序](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)。

`$_thread`


The thread number of the current thread. See [thread numbers](Threads.html#thread-numbers).

> 当前线程的线程号。参见[线程号](Threads.html#thread-numbers)。

`$_gthread`


The global number of the current thread. See [global thread numbers](Threads.html#global-thread-numbers).

> 当前线程的全局编号。请参见[全局线程编号](Threads.html#global-thread-numbers)。

`$_inferior_thread_count`


The number of live threads in the current inferior. See [Threads](Threads.html#Threads).

> 当前次级中的活动线程数。请参阅[线程](Threads.html#Threads)。

`$_gdb_major`

`$_gdb_minor`


The major and minor version numbers of the running [GDB] without errors caused by features unavailable in some of those versions.

> 运行中的GDB的主要和次要版本号，不受某些版本中无法使用的功能所引起的错误的影响。

`$_shell_exitcode`

`$_shell_exitsignal`


[GDB] automatically maintains the variables `$_shell_exitcode` and `$_shell_exitsignal` according to the exit status of the last launched command. These variables are set and used similarly to the variables `$_exitcode` and `$_exitsignal`.

> GDB 自动根据最近启动命令的退出状态来维护变量$_shell_exitcode和$_shell_exitsignal。这些变量的设置和使用方式与变量$_exitcode和$_exitsignal类似。

---

::: header
Next: [Convenience Funs](Convenience-Funs.html#Convenience-Funs)]
:::
