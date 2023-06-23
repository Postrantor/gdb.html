---
tip: translate by openai@2023-06-23 14:32:47
...
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

> 在一些操作系统，如GNU/Linux和Solaris，一个单独的程序可能有多个执行*线程*。线程的精确语义因操作系统而异，但通常一个程序的线程类似于多个进程---除了它们共享一个地址空间（也就是说，它们都可以检查和修改相同的变量）。另一方面，每个线程都有自己的寄存器和执行堆栈，以及可能的私有内存。


[GDB] provides these facilities for debugging multi-thread programs:

> [GDB] 为调试多线程程序提供了这些功能：

- automatic notification of new threads
- '`thread thread-id`', a command to switch among threads
- '`info threads`', a command to inquire about existing threads
- '`thread apply [thread-id-list | all] args`', a command to apply a command to a list of threads
- thread-specific breakpoints
- '`set print thread-events`', which controls printing of messages on thread start and exit.

- '`set libthread-db-search-path path`', which lets the user specify which `libthread_db` to use if the default choice isn't compatible with the program.

> 设置libthread-db-search-path路径，如果默认选择与程序不兼容，可以让用户指定使用哪个libthread_db。


The [GDB] takes control, one thread in particular is always the focus of debugging. This thread is called the *current thread*. Debugging commands show program information from the perspective of the current thread.

> 调试器（GDB）控制程序的执行，其中一个线程总是调试的焦点。这个线程被称为当前线程。调试命令从当前线程的角度显示程序信息。


Whenever [GDB]/Linux, you might see

> 无论何时使用GDB/Linux，你都可能会看到

::: smallexample

```bash
[New Thread 0x41e02940 (LWP 25582)]
```

:::


when [GDB]', with no further qualifier.

> 当使用GDB时


For debugging purposes, [GDB] associates its own thread number ---always a single integer---with each thread of an inferior. This number is unique between all threads of an inferior, but not unique between threads of different inferiors.

> 为了调试目的，GDB将自己的线程号---总是一个整数---与每个下级线程相关联。此号码在同一下级的所有线程之间是唯一的，但在不同下级的线程之间不是唯一的。


You can refer to a given thread in an inferior using the qualified `inferior-num` infers you're referring to a thread of the current inferior.

> 你可以使用合格的`inferior-num`引用当前inferior中的线程来参考给定的线程。


Until you create a second inferior, [GDB] form to refer to threads of inferior 1, the initial inferior.

> 直到你创建第二个次要的[GDB]形式来引用第一个次要的线程，初始次要。


Some commands accept a space-separated *thread ID list* as argument. A list element can be:

> 一些命令接受一个以空格分隔的*线程ID列表*作为参数。列表元素可以是：


1. A thread ID as shown in the first field of the '`info threads`'.

> 1. 作为“info threads”第一个字段中显示的线程ID。

2. A range of thread numbers, again with or without an inferior qualifier, as in `inf`'.

> 一系列线号，可以带有或不带下限限定符，例如`inf`。

3. All threads of an inferior, specified with a star wildcard, with or without an inferior qualifier, as in `inf`') or `*`. The former refers to all threads of the given inferior, and the latter form without an inferior qualifier refers to all threads of the current inferior.

> 所有使用星号通配符指定的次级线程，无论是否带有次级限定符，例如`inf`或`*`，前者指的是给定次级的所有线程，而后者不带次级限定符则指的是当前次级的所有线程。


For example, if the current inferior is 1, and inferior 7 has one thread with ID 7.1, the thread list '`1 2-3 4.5 6.7-9 7.*`'.

> 例如，如果当前的下级是1，而下级7有一个线程ID为7.1，那么线程列表为“1 2-3 4.5 6.7-9 7.*”。


In addition to a *per-inferior* number, each thread is also assigned a unique *global* number, also known as *global thread ID*, a single integer. Unlike the thread number component of the thread ID, no two threads have the same global ID, even when you're debugging multiple inferiors.

> 除了每个线程的比例较低的编号，每个线程还分配了一个唯一的全局编号，也称为全局线程ID，是一个整数。与线程ID的线程号组件不同，即使在调试多个比较低的情况下，也没有两个线程具有相同的全局ID。


From [GDB] assigns a thread number to the program's "main thread" even if the program is not multi-threaded.

> 从GDB开始，即使程序不是多线程的，也会为程序的“主线程”分配一个线程号。


The debugger convenience variables '`$_thread`' contains the number of live threads in the current inferior. See [Convenience Variables](Convenience-Vars.html#Convenience-Vars), for general information on convenience variables.

> 调试器便利变量 '`$_thread`' 包含当前次级中活动线程的数量。有关便利变量的一般信息，请参阅[便利变量](Convenience-Vars.html#Convenience-Vars)。


When running in non-stop mode (see [Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)), where new threads can be created, and existing threads exit, at any time, '`$_inferior_thread_count`' could return a different value each time it is evaluated.

> 当以非停止模式运行（请参见[非停止模式](Non_002dStop-Mode.html#Non_002dStop-Mode))，可以随时创建新线程和退出现有线程时，'$_inferior_thread_count' 每次被评估时可能会返回不同的值。


If [GDB] detects the program is multi-threaded, it augments the usual message about stopping at a breakpoint with the ID and name of the thread that hit the breakpoint.

> 如果GDB检测到程序是多线程的，它会在报告停在断点处的消息中增加该线程的ID和名称。

::: smallexample

```bash
Thread 2 "client" hit Breakpoint 1, send_message () at client.c:68
```

:::


Likewise when the program receives a signal:

> 同样，当程序接收到信号时：

::: smallexample

```bash
Thread 1 "main" received signal SIGINT, Interrupt.
```

:::

`info threads [-gid] [thread-id-list]`


Display information about one or more threads. With no arguments displays information about all threads. You can specify the list of threads that you want to display using the thread ID list syntax (see [thread ID lists](#thread-ID-lists)).

> 显示一个或多个线程的信息。不带参数时显示所有线程的信息。您可以使用线程ID列表语法（参见[线程ID列表]（＃线程ID列表））指定要显示的线程列表。


[GDB] displays for each thread (in this order):

> GDB显示每个线程（按此顺序）：


1. the per-inferior thread number assigned by [GDB]

> 1. GDB 所分配的每个线程号

2. the global thread number assigned by [GDB]' option was specified

> 通过[GDB]指定的全局线程号

3. the target system's thread identifier (`systag`)

> 目标系统的线程标识符（`systag`）

4. the thread's name, if one is known. A thread can either be named by the user (see `thread name`, below), or, in some cases, by the program itself.

> 线程的名称，如果已知的话。线程可以由用户命名（参见下面的“线程名称”），或者在某些情况下，由程序本身命名。

5. the current stack frame summary for that thread

> 当前线程的堆栈帧摘要


An asterisk '`*` thread number indicates the current thread.

> 一个星号'*'线程号表示当前线程。

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

> 如果你在调试多个次级程序，[GDB]就会显示出来。


If you specify the '`-gid` displays a column indicating each thread's global thread ID:

> 如果您指定'-gid'，将显示一列，指示每个线程的全局线程ID：

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

> 在Solaris上，您可以使用Solaris特定的命令显示更多有关用户线程的信息：

`maint info sol-threads`

:

```
Display info on Solaris user threads.
```

`thread thread-id`


Make thread ID `thread-id`').

> 制作线程ID `thread-id`


[GDB] responds by displaying the system identifier of the thread you selected, and its current stack frame summary:

> [GDB] 回应显示您选择的线程的系统标识符及其当前的堆栈帧摘要：

::: smallexample

```bash
(gdb) thread 2
[Switching to thread 2 (Thread 0xb7fdab70 (LWP 12747))]
#0  some_function (ignore=0x0) at example.c:8
8       printf ("hello\n");
```

:::


As with the '`[New …]`' depends on your system's conventions for identifying threads.

> 随着'[新...]'取决于你的系统用于识别线程的惯例。

`thread apply [thread-id-list | all [-ascending]] [flag]… command`


The `thread apply` command allows you to apply the named `command`.

> 命令`thread apply`允许你应用指定的`命令`。


The `flag` must start with a `-` directly followed by one letter in `qcs`. If several flags are provided, they must be given individually, such as `-c -q`.

> 标志必须以`-`开头，后面直接跟一个`qcs`中的字母。如果提供了多个标志，它们必须分开给出，如`-c -q`。


By default, [GDB] will abort `thread apply`. The following flags can be used to fine-tune this behavior:

> 默认情况下，GDB会中止`thread apply`。 以下标志可用于微调此行为：

`-c`


:   The flag `-c`, which stands for '`continue` to be displayed, and the execution of `thread apply` then continues.

> 标志`-c`代表"继续"显示，然后继续执行`thread apply`。

`-s`


:   The flag `-s`, which stands for '`silent` to be silently ignored. That is, the execution continues, but the thread information and errors are not printed.

> 标志`-s`代表“静默”，可以被静默忽略。也就是说，执行继续进行，但是线程信息和错误不会被打印出来。

`-q`


:   The flag `-q` ('`quiet`') disables printing the thread information.

> `标志'-q'（'quiet'）禁用打印线程信息。`


Flags `-c` and `-s` cannot be used together.

> 不能同时使用`-c`和`-s`标志。

`taas [option]… command`


Shortcut for `thread apply all -s [option]… command`. Applies `command` on all threads, ignoring errors and empty output.

> 快捷方式 `thread apply all -s [option]… command`。 对所有线程应用 `command`，忽略错误和空输出。


The `taas` command accepts the same options as the `thread apply all` command. See [thread apply all](#thread-apply-all).

> 命令`taas`接受与`thread apply all`命令相同的选项。详见[thread apply all](#thread-apply-all)。

`tfaas [option]… command`


Shortcut for `thread apply all -s -- frame apply all -s [option]… command`. Applies `command` successfully produced some output.

> 快捷方式：使用`thread apply all -s -- frame apply all -s [option]…` 命令成功执行`command`，并产生一些输出。


It can for example be used to print a local variable or a function argument without knowing the thread or frame where this variable or argument is, using:

> 它可以用来打印局部变量或函数参数，而无需知道该变量或参数所在的线程或帧，方法是：

::: smallexample

```bash
(gdb) tfaas p some_local_var_i_do_not_remember_where_it_is
```

:::


The `tfaas` command accepts the same options as the `frame apply` command. See [frame apply](Frame-Apply.html#Frame-Apply).

> 命令`tfaas`接受与命令`frame apply`相同的选项。请参阅[frame apply](Frame-Apply.html#Frame-Apply)。

`thread name [name]`


This command assigns a name to the current thread. If no argument is given, any existing user-specified name is removed. The thread name appears in the '`info threads`' display.

> 这个命令为当前线程指定一个名称。如果没有指定参数，则会删除任何现有的用户指定的名称。线程名称会出现在 '`info threads`' 显示中。


On some systems, such as [GNU] to once again display the system-specified name.

> 在一些系统（比如GNU）上，再次显示系统指定的名称。

`thread find [regexp]`


Search for and display thread ids whose name or `systag` matches the supplied regular expression.

> 搜索并显示名称或`systag`与提供的正则表达式匹配的线程ID。


As well as being the complement to the '`thread name` is the LWP id.

> `"thread name"是LWP ID的补充。`

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

> 命令 `set print thread-events` 允许您启用或禁用在 [GDB] 注意到新线程已启动或线程已退出时打印消息的功能。默认情况下，如果目标支持检测这些事件，则会打印这些消息。请注意，并非所有目标都可以禁用这些消息。

`show print thread-events`


Show whether messages will be printed when [GDB] detects that threads have started and exited.

> 当GDB检测到线程已经启动和退出时，显示消息是否会被打印。


See [Stopping and Starting Multi-thread Programs](Thread-Stops.html#Thread-Stops), for more information about how [GDB] behaves when you stop and start programs with multiple threads.

> 请参阅[停止和启动多线程程序](Thread-Stops.html#Thread-Stops)，了解有关[GDB]在停止和启动具有多个线程的程序时的行为的更多信息。


See [Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints), for information about watchpoints in programs with multiple threads.

> 请参阅[设置监视点](Set-Watchpoints.html#Set-Watchpoints)，了解关于多线程程序中的监视点的信息。

`set libthread-db-search-path [path]`


If this variable is set, `path`/Linux and Solaris systems). Internally, the default value comes from the `LIBTHREAD_DB_SEARCH_PATH` macro.

> 如果设置了此变量，`path`/Linux和Solaris系统将使用内部默认值，该默认值来自`LIBTHREAD_DB_SEARCH_PATH`宏。


On [GNU]' (see [libthread_db.so.1 file](libthread_005fdb_002eso_002e1-file.html#libthread_005fdb_002eso_002e1-file)).

> 在GNU上


A special entry '`$sdir`' (see [libthread_db.so.1 file](libthread_005fdb_002eso_002e1-file.html#libthread_005fdb_002eso_002e1-file)).

> 特殊条目'`$sdir`'（参见[libthread_db.so.1 文件]（libthread_005fdb_002eso_002e1-file.html#libthread_005fdb_002eso_002e1-file））。


A special entry '`$pdir`' refers to the directory from which `libpthread` was loaded in the inferior process.

> '特殊条目'$pdir'指的是从下级进程加载`libpthread`的目录。


For any `libthread_db` library [GDB] will issue a warning and thread debugging will be disabled.

> 对于任何`libthread_db`库，[GDB]都会发出警告，线程调试将被禁用。


Setting `libthread-db-search-path` is currently implemented only on some platforms.

> 设置`libthread-db-search-path`目前只在一些平台上实现。

`show libthread-db-search-path`


Display current libthread_db search path.

> 显示当前libthread_db搜索路径。

`set debug libthread-db`

`show debug libthread-db`


Turns on or off display of `libthread_db`-related events. Use `1` to enable, `0` to disable.

> 打开或关闭`libthread_db`相关事件的显示。使用`1`来启用，使用`0`来禁用。

`set debug threads [on|off]`

`show debug threads`


When '`on` will print additional messages when threads are created and deleted.

> 当'on'时，在创建和删除线程时会打印额外的消息。

---

::: header
Next: [Forks](Forks.html#Forks)]
:::
