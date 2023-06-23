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

`ftrace locspec [ if cond ]`

The `ftrace` command sets a fast tracepoint. For targets that support them, fast tracepoints will use a more efficient but possibly less general technique to trigger data collection, such as a jump instruction instead of a trap, or some sort of hardware support. It may not be possible to create a fast tracepoint at the desired location, in which case the command will exit with an explanatory message.

[GDB] handles arguments to `ftrace` exactly as for `trace`.

On 32-bit x86-architecture systems, fast tracepoints normally need to be placed at an instruction that is 5 bytes or longer, but can be placed at 4-byte instructions if the low 64K of memory of the target program is available to install trampolines. Some Unix-type systems, such as [GNU] use this area by doing a `sysctl` command to set the `mmap_min_addr` kernel parameter, as in

::: example

```example
sudo sysctl -w vm.mmap_min_addr=32768
```

:::

which sets the low address to 32K, which leaves plenty of room for trampolines. The minimum address should be set to a page boundary.

`strace [locspec | -m marker] [ if cond ]`

The `strace` command sets a static tracepoint. For targets that support it, setting a static tracepoint probes a static instrumentation point, or marker, found at the code locations that result from resolving `locspec`. It may not be possible to set a static tracepoint at the desired code location, in which case the command will exit with an explanatory message.

[GDB]' field of the `info static-tracepoint-markers` command output. See [Listing Static Tracepoint Markers](Listing-Static-Tracepoint-Markers.html#Listing-Static-Tracepoint-Markers). For example, in the following small program using the UST tracing engine:

::: smallexample

```bash
main ()
{
  trace_mark(ust, bar33, "str %s", "FOOBAZ");
}
```

:::

the marker id is composed of joining the first two arguments to the `trace_mark` call with a slash, which translates to:

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

You can inspect this data when analyzing the trace buffer, by printing the \$_sdata variable like any other variable available to [GDB]. See [Tracepoint Action Lists](Tracepoint-Actions.html#Tracepoint-Actions).

The convenience variable `$tpnum` records the tracepoint number of the most recently set tracepoint.

`delete tracepoint [num]`

Permanently delete one or more tracepoints. With no argument, the default is to delete all tracepoints. Note that the regular `delete` command can remove tracepoints also.

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
