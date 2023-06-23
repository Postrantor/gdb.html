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

`$regs`

:   Collect all registers.

`$args`

:   Collect all function arguments.

`$locals`

:   Collect all local variables.

`$_ret`

:   Collect the return address. This is helpful if you want to see more of a backtrace.

```
*Note:* The return address location can not always be reliably determined up front, and the wrong address / registers may end up collected instead. On some architectures the reliability is higher for tracepoints at function entry, while on others it's the opposite. When this happens, backtracing will stop because the return address is found unavailable (unless another collect rule happened to match it).
```

`$_probe_argc`

:   Collects the number of arguments from the static probe at which the tracepoint is located. See [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points).

`$_probe_argn`

:   `n` th argument from the static probe at which the tracepoint is located. See [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points).

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

The optional `mods`'.

The command `info scope` (see [info scope](Symbols.html#Symbols)) is particularly useful for figuring out what data to collect.



`teval expr1, expr2, …`

Evaluate the given expressions when the tracepoint is hit. This command accepts a comma-separated list of expressions. The results are discarded, so this is mainly useful for assigning values to trace state variables (see [Trace State Variables](Trace-State-Variables.html#Trace-State-Variables)) without adding those values to the trace buffer, as would be the case if the `collect` action were used.



`while-stepping n`

Perform `n` single-step instruction traces after the tracepoint, collecting new data after each step. The `while-stepping` command is followed by the list of what to collect while stepping (followed by its own `end` command):

::: smallexample

```bash
> while-stepping 12
  > collect $regs, myglobal
  > end
>
```

:::

Note that `$pc` is not automatically collected by `while-stepping`; you need to explicitly collect that register if you need it. You may abbreviate `while-stepping` as `ws` or `stepping`.

`set default-collect expr1, expr2, …`

This variable is a list of expressions to collect at each tracepoint hit. It is effectively an additional `collect` action prepended to every tracepoint action list. The expressions are parsed individually for each tracepoint, so for instance a variable named `xyz` may be interpreted as a global for one tracepoint, and a local for another, as appropriate to the tracepoint's location.

`show default-collect`

Show the list of expressions that are collected by default at each tracepoint hit.

---

::: header
Next: [Listing Tracepoints](Listing-Tracepoints.html#Listing-Tracepoints)]
:::
