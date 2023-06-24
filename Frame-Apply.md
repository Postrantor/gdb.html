---
tip: translate by openai@2023-06-23 21:19:30
...
---
description: Frame Apply (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Frame Apply (Debugging with GDB)
lang: en
resource-type: document
title: Frame Apply (Debugging with GDB)
---
::: header
Next: [Frame Filter Management](Frame-Filter-Management.html#Frame-Filter-Management)]
:::

---

### 8.5 Applying a Command to Several Frames.

`frame apply [all | count | -count | level level…] [option]… command`


:   The `frame apply` command allows you to apply the named `command` to one or more frames.

> 命令`frame apply`允许您将指定的命令应用于一个或多个框架。

```
`all`

:   Specify `all` to apply `command` to all frames.

`count`

:   Use `count` is a positive number.

`-count`

:   Use `-count` is a positive number.

`level`

:   Use `level` to apply `command` for the frames at levels 2, 3, 4, 6, 7, 8, and then again on frame at level 3.

Note that the frames on which `frame apply` applies a command are also influenced by the `set backtrace` settings such as `set backtrace past-main` and `set backtrace limit N`. See [Backtraces](Backtrace.html#Backtrace).

The `frame apply` command also supports a number of options that allow overriding relevant `set backtrace` settings:

`-past-main [on`\|`off`]

:   Whether backtraces should continue past `main`. Related setting: [set backtrace past-main](Backtrace.html#set-backtrace-past_002dmain).

`-past-entry [on`\|`off`]

:   Whether backtraces should continue past the entry point of a program. Related setting: [set backtrace past-entry](Backtrace.html#set-backtrace-past_002dentry).

By default, [GDB] will abort `frame apply`. The following options can be used to fine-tune these behaviors:

`-c`

:   The flag `-c`, which stands for '`continue` to be displayed, and the execution of `frame apply` then continues.

`-s`

:   The flag `-s`, which stands for '`silent` to be silently ignored. That is, the execution continues, but the frame information and errors are not printed.

`-q`

:   The flag `-q` ('`quiet`') disables printing the frame information.

The following example shows how the flags `-c` and `-s` are working when applying the command `p j` to all frames, where variable `j` can only be successfully printed in the outermost `#1 main` frame.

::: smallexample
``` smallexample
(gdb) frame apply all p j
#0  some_function (i=5) at fun.c:4
No symbol "j" in current context.
(gdb) frame apply all -c p j
#0  some_function (i=5) at fun.c:4
No symbol "j" in current context.
#1  0x565555fb in main (argc=1, argv=0xffffd2c4) at fun.c:11
$1 = 5
(gdb) frame apply all -s p j
#1  0x565555fb in main (argc=1, argv=0xffffd2c4) at fun.c:11
$2 = 5
(gdb)
```

:::

By default, '`frame apply`', prints the frame location information before the command output:

::: smallexample

```bash
(gdb) frame apply all p $sp
#0  some_function (i=5) at fun.c:4
$4 = (void *) 0xffffd1e0
#1  0x565555fb in main (argc=1, argv=0xffffd2c4) at fun.c:11
$5 = (void *) 0xffffd1f0
(gdb)
```

:::

If the flag `-q` is given, no frame information is printed:

::: smallexample

```bash
(gdb) frame apply all -q p $sp
$12 = (void *) 0xffffd1e0
$13 = (void *) 0xffffd1f0
(gdb)
```

:::

```



`faas command`


Shortcut for `frame apply all -s command`. Applies `command` on all frames, ignoring errors and empty output.

> 给所有帧应用`command`的快捷方式，忽略错误和空输出。


It can for example be used to print a local variable or a function argument without knowing the frame where this variable or argument is, using:

> 它可以用来打印局部变量或函数参数，而无需知道这个变量或参数所在的框架，方法是：

::: smallexample

```bash
(gdb) faas p some_local_var_i_do_not_remember_where_it_is
```

:::


The `faas` command accepts the same options as the `frame apply` command. See [frame apply](#Frame-Apply).

> `命令`faas`接受与`frame apply`命令相同的选项。请参见[frame apply](#Frame-Apply)。`


Note that the command `tfaas command` applies `command` on all frames of all threads. See See [Threads](Threads.html#Threads).

> 注意，命令`tfaas command`会在所有线程的所有帧上应用`command`。请参见[线程](Threads.html#Threads)。

---

::: header
Next: [Frame Filter Management](Frame-Filter-Management.html#Frame-Filter-Management)]
:::
