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

Convenience variables are prefixed with '`$`'. See [Value History](Value-History.html#Value-History).)

You can save a value in a convenience variable with an assignment expression, just as you would set a variable in your program. For example:

::: smallexample

```bash
set $foo = *object_ptr
```

:::

would save in `$foo` the value contained in the object pointed to by `object_ptr`.

Using a convenience variable for the first time creates it, but its value is `void` until you assign a new value. You can alter the value with another assignment at any time.

Convenience variables have no fixed types. You can assign a convenience variable any type of value, including structures and arrays, even if that variable already has a value of a different type. The convenience variable, when used as an expression, has the type of its current value.

`show convenience`

Print a list of convenience variables used so far, and their values, as well as a list of the convenience functions. Abbreviated `show conv`.

`init-if-undefined $variable = expression`

Set a convenience variable if it has not already been set. This is useful for user-defined commands that keep some state. It is similar, in concept, to using local static variables with initializers in C (except that convenience variables are global). It can also be used to allow users to override default values used in a command script.

If the variable is already defined then the expression is not evaluated so any side-effects do not occur.

One of the ways to use a convenience variable is as a counter to be incremented or a pointer to be advanced. For example, to print a field from successive elements of an array of structures:

::: smallexample

```bash
set $i = 0
print bar[$i++]->contents
```

:::

Repeat that command by typing RET.

Some convenience variables are created automatically by [GDB] and given values likely to be useful.

`$_`

The variable `$_` is automatically set by the `x` command to the last address examined (see [Examining Memory](Memory.html#Memory)). Other commands which provide a default address for `x` to examine also set `$_` to that address; these commands include `info line` and `info breakpoint`. The type of `$_` is `void *` except when set by the `x` command, in which case it is a pointer to the type of `$__`.

`$__`

The variable `$__` is automatically set by the `x` command to the value found in the last address examined. Its type is chosen to match the format in which the data was printed.

`$_exitcode`

When the program being debugged terminates normally, [GDB] automatically sets this variable to the exit code of the program, and resets `$_exitsignal` to `void`.

`$_exitsignal`

When the program being debugged dies due to an uncaught signal, [GDB] automatically sets this variable to that signal's number, and resets `$_exitcode` to `void`.

To distinguish between whether the program being debugged has exited (i.e., `$_exitcode` is not `void`) or signalled (i.e., `$_exitsignal` is not `void`), the convenience function `$_isvoid` can be used (see [Convenience Functions](Convenience-Funs.html#Convenience-Funs)). For example, considering the following source code:

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

`$_ada_exception`

The variable `$_ada_exception` is set to the address of the exception being caught or thrown at an Ada exception-related catchpoint. See [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints).

`$_probe_argc`

`$_probe_arg0…$_probe_arg11`

Arguments to a static probe. See [Static Probe Points](Static-Probe-Points.html#Static-Probe-Points).

`$_sdata`

The variable `$_sdata` contains extra collected static tracepoint data. See [Tracepoint Action Lists](Tracepoint-Actions.html#Tracepoint-Actions). Note that `$_sdata` could be empty, if not inspecting a trace buffer, or if extra static tracepoint data has not been collected.

`$_siginfo`

The variable `$_siginfo` contains extra signal information (see [extra signal information](Signals.html#extra-signal-information)). Note that `$_siginfo` could be empty, if the application has not yet received any signals. For example, it will be empty before you execute the `run` command.

`$_tlb`

The variable `$_tlb` is automatically set when debugging applications running on MS-Windows in native mode or connected to gdbserver that supports the `qGetTIBAddr` request. See [General Query Packets](General-Query-Packets.html#General-Query-Packets). This variable contains the address of the thread information block.

`$_inferior`

The number of the current inferior. See [Debugging Multiple Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs).

`$_thread`

The thread number of the current thread. See [thread numbers](Threads.html#thread-numbers).

`$_gthread`

The global number of the current thread. See [global thread numbers](Threads.html#global-thread-numbers).

`$_inferior_thread_count`

The number of live threads in the current inferior. See [Threads](Threads.html#Threads).

`$_gdb_major`

`$_gdb_minor`

The major and minor version numbers of the running [GDB] without errors caused by features unavailable in some of those versions.

`$_shell_exitcode`

`$_shell_exitsignal`

[GDB] automatically maintains the variables `$_shell_exitcode` and `$_shell_exitsignal` according to the exit status of the last launched command. These variables are set and used similarly to the variables `$_exitcode` and `$_exitsignal`.

---

::: header
Next: [Convenience Funs](Convenience-Funs.html#Convenience-Funs)]
:::
