---
tip: translate by openai@2023-06-23 20:05:52
...
---
description: Create and Delete Tracepoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Create and Delete Tracepoints (Debugging with GDB)
lang: en
resource-type: document
title: Create and Delete Tracepoints (Debugging with GDB)
---
::: header
Next: [Enable and Disable Tracepoints](Enable-and-Disable-Tracepoints.html#Enable-and-Disable-Tracepoints)]
:::

---

#### 13.1.1 Create and Delete Tracepoints

`trace locspec`


The `trace` command is very similar to the `break` command. Its argument `locspec` is disconnected.

> 命令`trace`与命令`break`非常相似，其参数`locspec`已断开连接。

Here are some examples of using the `trace` command:

::: smallexample

```bash
(gdb) trace foo.c:121    // a source file and line number

(gdb) trace +2           // 2 lines forward

(gdb) trace my_function  // first source line of function

(gdb) trace *my_function // EXACT start address of function

(gdb) trace *0x2117c4    // an address
```

:::

You can abbreviate `trace` as `tr`.

`trace locspec if cond`


Set a tracepoint with condition `cond` evaluates as true. See [Tracepoint Conditions](Tracepoint-Conditions.html#Tracepoint-Conditions), for more information on tracepoint conditions.

> 设置一个断点，当`cond`满足时触发。更多关于断点条件的信息，请参阅[断点条件](Tracepoint-Conditions.html#Tracepoint-Conditions)。

`ftrace locspec [ if cond ]`


The `ftrace` command sets a fast tracepoint. For targets that support them, fast tracepoints will use a more efficient but possibly less general technique to trigger data collection, such as a jump instruction instead of a trap, or some sort of hardware support. It may not be possible to create a fast tracepoint at the desired location, in which case the command will exit with an explanatory message.

> 命令`ftrace`设置快速跟踪点。对于支持它们的目标，快速跟踪点将使用更有效但可能不太一般的技术来触发数据收集，如使用跳转指令而不是陷阱，或者某种硬件支持。可能无法在所需位置创建快速跟踪点，在这种情况下，该命令将使用解释性消息退出。

[GDB] handles arguments to `ftrace` exactly as for `trace`.


On 32-bit x86-architecture systems, fast tracepoints normally need to be placed at an instruction that is 5 bytes or longer, but can be placed at 4-byte instructions if the low 64K of memory of the target program is available to install trampolines. Some Unix-type systems, such as [GNU] use this area by doing a `sysctl` command to set the `mmap_min_addr` kernel parameter, as in

> 在32位x86架构系统上，快速跟踪点通常需要放置在5个字节或更长的指令上，但如果目标程序的低64K内存可用于安装跳转，则可以放置在4字节指令上。一些类Unix系统，例如[GNU]，通过执行`sysctl`命令来设置`mmap_min_addr`内核参数来使用这一区域，如

::: example

```example
sudo sysctl -w vm.mmap_min_addr=32768
```

:::


which sets the low address to 32K, which leaves plenty of room for trampolines. The minimum address should be set to a page boundary.

> 将低地址设置为32K，为跳跃提供了充足的空间。最低地址应设置为页面边界。

`strace [locspec | -m marker] [ if cond ]`


The `strace` command sets a static tracepoint. For targets that support it, setting a static tracepoint probes a static instrumentation point, or marker, found at the code locations that result from resolving `locspec`. It may not be possible to set a static tracepoint at the desired code location, in which case the command will exit with an explanatory message.

> `strace` 命令设置一个静态跟踪点。对于支持它的目标，设置一个静态跟踪点会探测从解析`locspec`得到的代码位置处找到的静态插装点或标记。可能无法在所需的代码位置设置静态跟踪点，在这种情况下，该命令将以一条解释性消息退出。


[GDB]' field of the `info static-tracepoint-markers` command output. See [Listing Static Tracepoint Markers](Listing-Static-Tracepoint-Markers.html#Listing-Static-Tracepoint-Markers). For example, in the following small program using the UST tracing engine:

> [GDB] 是指`info static-tracepoint-markers`命令输出的字段。请参阅[Listing Static Tracepoint Markers](Listing-Static-Tracepoint-Markers.html#Listing-Static-Tracepoint-Markers)。例如，在使用UST跟踪引擎的以下小程序中：

::: smallexample

```bash
main ()
{
  trace_mark(ust, bar33, "str %s", "FOOBAZ");
}
```

:::


the marker id is composed of joining the first two arguments to the `trace_mark` call with a slash, which translates to:

> 标记ID由调用`trace_mark`的前两个参数通过斜杠连接而成。

::: smallexample

```bash
(gdb) info static-tracepoint-markers
Cnt Enb ID         Address            What
1   n   ust/bar33  0x0000000000400ddc in main at stexample.c:22
         Data: "str %s"
[etc...]
```

:::

so you may probe the marker above with:

::: smallexample

```bash
(gdb) strace -m ust/bar33
```

:::


Static tracepoints accept an extra collect action --- `collect $_sdata`. This collects arbitrary user data passed in the probe point call to the tracing library. In the UST example above, you'll see that the third argument to `trace_mark` is a printf-like format string. The user data is then the result of running that formatting string against the following arguments. Note that `info static-tracepoint-markers` command output lists that format string in the '`Data:`' field.

> 静态跟踪点接受额外的收集操作---`collect $_sdata`。这会收集在探测点调用到跟踪库时传递的任意用户数据。在上面的UST示例中，您会看到`trace_mark`的第三个参数是一个类似printf的格式字符串。然后，用户数据就是对以下参数运行该格式字符串的结果。请注意，`info static-tracepoint-markers`命令输出中列出的'`Data:`'字段中包含该格式字符串。


You can inspect this data when analyzing the trace buffer, by printing the \$_sdata variable like any other variable available to [GDB]. See [Tracepoint Action Lists](Tracepoint-Actions.html#Tracepoint-Actions).

> 您可以在分析跟踪缓冲区时，通过像其他[GDB]可用变量一样打印\$_sdata变量来检查此数据。请参见[跟踪点操作列表](Tracepoint-Actions.html#Tracepoint-Actions)。


The convenience variable `$tpnum` records the tracepoint number of the most recently set tracepoint.

> 变量$tpnum记录了最近设置的断点的断点号。

`delete tracepoint [num]`


Permanently delete one or more tracepoints. With no argument, the default is to delete all tracepoints. Note that the regular `delete` command can remove tracepoints also.

> 永久删除一个或多个跟踪点。如果没有参数，默认情况下将删除所有跟踪点。注意，常规的“delete”命令也可以删除跟踪点。

Examples:

::: smallexample

```bash
(gdb) delete trace 1 2 3 // remove three tracepoints

(gdb) delete trace       // remove all tracepoints
```

:::

You can abbreviate this command as `del tr`.

---

::: header
Next: [Enable and Disable Tracepoints](Enable-and-Disable-Tracepoints.html#Enable-and-Disable-Tracepoints)]
:::
