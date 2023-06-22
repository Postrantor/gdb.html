---
description: Threads (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Threads (Debugging with GDB)
lang: en
resource-type: document
title: Threads (Debugging with GDB)
---
::: header
Next: [Forks](Forks.html#Forks)]
:::

---

### 4.10 Debugging Programs with Multiple Threads

In some operating systems, such as GNU/Linux and Solaris, a single program may have more than one *thread* of execution. The precise semantics of threads differ from one operating system to another, but in general the threads of a single program are akin to multiple processes---except that they share one address space (that is, they can all examine and modify the same variables). On the other hand, each thread has its own registers and execution stack, and perhaps private memory.

[GDB] provides these facilities for debugging multi-thread programs:

- automatic notification of new threads
- '`thread thread-id`', a command to switch among threads
- '`info threads`', a command to inquire about existing threads
- '`thread apply [thread-id-list | all] args`', a command to apply a command to a list of threads
- thread-specific breakpoints
- '`set print thread-events`', which controls printing of messages on thread start and exit.
- '`set libthread-db-search-path path`', which lets the user specify which `libthread_db` to use if the default choice isn't compatible with the program.

The [GDB] takes control, one thread in particular is always the focus of debugging. This thread is called the *current thread*. Debugging commands show program information from the perspective of the current thread.

Whenever [GDB]/Linux, you might see

::: smallexample

```bash
[New Thread 0x41e02940 (LWP 25582)]
```

:::

when [GDB]', with no further qualifier.

For debugging purposes, [GDB] associates its own thread number ---always a single integer---with each thread of an inferior. This number is unique between all threads of an inferior, but not unique between threads of different inferiors.

You can refer to a given thread in an inferior using the qualified `inferior-num` infers you're referring to a thread of the current inferior.

Until you create a second inferior, [GDB] form to refer to threads of inferior 1, the initial inferior.

Some commands accept a space-separated *thread ID list* as argument. A list element can be:

1. A thread ID as shown in the first field of the '`info threads`'.
2. A range of thread numbers, again with or without an inferior qualifier, as in `inf`'.
3. All threads of an inferior, specified with a star wildcard, with or without an inferior qualifier, as in `inf`') or `*`. The former refers to all threads of the given inferior, and the latter form without an inferior qualifier refers to all threads of the current inferior.

For example, if the current inferior is 1, and inferior 7 has one thread with ID 7.1, the thread list '`1 2-3 4.5 6.7-9 7.*`'.

In addition to a *per-inferior* number, each thread is also assigned a unique *global* number, also known as *global thread ID*, a single integer. Unlike the thread number component of the thread ID, no two threads have the same global ID, even when you're debugging multiple inferiors.

From [GDB] assigns a thread number to the program's "main thread" even if the program is not multi-threaded.

The debugger convenience variables '`$_thread`' contains the number of live threads in the current inferior. See [Convenience Variables](Convenience-Vars.html#Convenience-Vars), for general information on convenience variables.

When running in non-stop mode (see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)), where new threads can be created, and existing threads exit, at any time, '`$_inferior_thread_count`' could return a different value each time it is evaluated.

If [GDB] detects the program is multi-threaded, it augments the usual message about stopping at a breakpoint with the ID and name of the thread that hit the breakpoint.

::: smallexample

```bash
Thread 2 "client" hit Breakpoint 1, send_message () at client.c:68
```

:::

Likewise when the program receives a signal:

::: smallexample

```bash
Thread 1 "main" received signal SIGINT, Interrupt.
```

:::

`info threads [-gid] [thread-id-list]`

Display information about one or more threads. With no arguments displays information about all threads. You can specify the list of threads that you want to display using the thread ID list syntax (see [thread ID lists](#thread-ID-lists)).

[GDB] displays for each thread (in this order):

1. the per-inferior thread number assigned by [GDB]
2. the global thread number assigned by [GDB]' option was specified
3. the target system's thread identifier (`systag`)
4. the thread's name, if one is known. A thread can either be named by the user (see `thread name`, below), or, in some cases, by the program itself.
5. the current stack frame summary for that thread

An asterisk '`*` thread number indicates the current thread.

For example,

::: smallexample

```bash
(gdb) info threads
  Id   Target Id             Frame
* 1    process 35 thread 13  main (argc=1, argv=0x7ffffff8)
  2    process 35 thread 23  0x34e5 in sigpause ()
  3    process 35 thread 27  0x34e5 in sigpause ()
    at threadtest.c:68
```

:::

If you're debugging multiple inferiors, [GDB] is shown.

If you specify the '`-gid` displays a column indicating each thread's global thread ID:

::: smallexample

```bash
(gdb) info threads
  Id   GId  Target Id             Frame
  1.1  1    process 35 thread 13  main (argc=1, argv=0x7ffffff8)
  1.2  3    process 35 thread 23  0x34e5 in sigpause ()
  1.3  4    process 35 thread 27  0x34e5 in sigpause ()
* 2.1  2    process 65 thread 1   main (argc=1, argv=0x7ffffff8)
```

:::

On Solaris, you can display more information about user threads with a Solaris-specific command:

`maint info sol-threads`

:

```
Display info on Solaris user threads.
```

`thread thread-id`

Make thread ID `thread-id`').

[GDB] responds by displaying the system identifier of the thread you selected, and its current stack frame summary:

::: smallexample

```bash
(gdb) thread 2
[Switching to thread 2 (Thread 0xb7fdab70 (LWP 12747))]
#0  some_function (ignore=0x0) at example.c:8
8       printf ("hello\n");
```

:::

As with the '`[New …]`' depends on your system's conventions for identifying threads.

`thread apply [thread-id-list | all [-ascending]] [flag]… command`

The `thread apply` command allows you to apply the named `command`.

The `flag` must start with a `-` directly followed by one letter in `qcs`. If several flags are provided, they must be given individually, such as `-c -q`.

By default, [GDB] will abort `thread apply`. The following flags can be used to fine-tune this behavior:

`-c`

:   The flag `-c`, which stands for '`continue` to be displayed, and the execution of `thread apply` then continues.

`-s`

:   The flag `-s`, which stands for '`silent` to be silently ignored. That is, the execution continues, but the thread information and errors are not printed.

`-q`

:   The flag `-q` ('`quiet`') disables printing the thread information.

Flags `-c` and `-s` cannot be used together.

`taas [option]… command`

Shortcut for `thread apply all -s [option]… command`. Applies `command` on all threads, ignoring errors and empty output.

The `taas` command accepts the same options as the `thread apply all` command. See [thread apply all](#thread-apply-all).

`tfaas [option]… command`

Shortcut for `thread apply all -s -- frame apply all -s [option]… command`. Applies `command` successfully produced some output.

It can for example be used to print a local variable or a function argument without knowing the thread or frame where this variable or argument is, using:

::: smallexample

```bash
(gdb) tfaas p some_local_var_i_do_not_remember_where_it_is
```

:::

The `tfaas` command accepts the same options as the `frame apply` command. See [frame apply](Frame-Apply.html#Frame-Apply).

`thread name [name]`

This command assigns a name to the current thread. If no argument is given, any existing user-specified name is removed. The thread name appears in the '`info threads`' display.

On some systems, such as [GNU] to once again display the system-specified name.

`thread find [regexp]`

Search for and display thread ids whose name or `systag` matches the supplied regular expression.

As well as being the complement to the '`thread name` is the LWP id.

::: smallexample

```bash
(gdb) thread find 26688
Thread 4 has target id 'Thread 0x41e02940 (LWP 26688)'
(gdb) info thread 4
  Id   Target Id         Frame 
  4    Thread 0x41e02940 (LWP 26688) 0x00000031ca6cd372 in select ()
```

:::

`set print thread-events`

`set print thread-events on`

`set print thread-events off`

The `set print thread-events` command allows you to enable or disable printing of messages when [GDB] notices that new threads have started or that threads have exited. By default, these messages will be printed if detection of these events is supported by the target. Note that these messages cannot be disabled on all targets.

`show print thread-events`

Show whether messages will be printed when [GDB] detects that threads have started and exited.

See [Stopping and Starting Multi-thread Programs](Thread-Stops.html#Thread-Stops), for more information about how [GDB] behaves when you stop and start programs with multiple threads.

See [Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints), for information about watchpoints in programs with multiple threads.

`set libthread-db-search-path [path]`

If this variable is set, `path`/Linux and Solaris systems). Internally, the default value comes from the `LIBTHREAD_DB_SEARCH_PATH` macro.

On [GNU]' (see [libthread_db.so.1 file](libthread_005fdb_002eso_002e1-file.html#libthread_005fdb_002eso_002e1-file)).

A special entry '`$sdir`' (see [libthread_db.so.1 file](libthread_005fdb_002eso_002e1-file.html#libthread_005fdb_002eso_002e1-file)).

A special entry '`$pdir`' refers to the directory from which `libpthread` was loaded in the inferior process.

For any `libthread_db` library [GDB] will issue a warning and thread debugging will be disabled.

Setting `libthread-db-search-path` is currently implemented only on some platforms.

`show libthread-db-search-path`

Display current libthread_db search path.

`set debug libthread-db`

`show debug libthread-db`

Turns on or off display of `libthread_db`-related events. Use `1` to enable, `0` to disable.

`set debug threads [on|off]`

`show debug threads`

When '`on` will print additional messages when threads are created and deleted.

---

::: header
Next: [Forks](Forks.html#Forks)]
:::
