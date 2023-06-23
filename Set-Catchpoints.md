---
tip: translate by openai@2023-06-23 13:00:44
...
---
description: Set Catchpoints (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Set Catchpoints (Debugging with GDB)
lang: en
resource-type: document
title: Set Catchpoints (Debugging with GDB)
---
::: header
Next: [Delete Breaks](Delete-Breaks.html#Delete-Breaks)]
:::

---

#### 5.1.3 Setting Catchpoints


You can use *catchpoints* to cause the debugger to stop for certain kinds of program events, such as C++ exceptions or the loading of a shared library. Use the `catch` command to set a catchpoint.

> 你可以使用*捕获点*来导致调试器停止某些类型的程序事件，例如C++异常或加载共享库。使用`catch`命令设置捕获点。

`catch event`


Stop when `event` can be any of the following:

> 停止，当`event`可以是以下任一个：

`throw [regexp]`
`rethrow [regexp]`
`catch [regexp]`

:

```
The throwing, re-throwing, or catching of a C++ exception.

If `regexp` is given, then only exceptions whose type matches the regular expression will be caught.



The convenience variable `$_exception` is available at an exception-related catchpoint, on some systems. This holds the exception being thrown.

There are currently some limitations to C++ exception handling in [GDB]:

-   The support for these commands is system-dependent. Currently, only systems using the '`gnu-v3`' C++ ABI (see [ABI](ABI.html#ABI)) are supported.
-   The regular expression feature and the `$_exception` convenience variable rely on the presence of some SDT probes in `libstdc++`. If these probes are not present, then these features cannot be used. These probes were first available in the GCC 4.8 release, but whether or not they are available in your GCC also depends on how it was built.
-   The `$_exception` convenience variable is only valid at the instruction at which an exception-related catchpoint is set.
-   When an exception-related catchpoint is hit, [GDB] stops at a location in the system library which implements runtime exception support for C++, usually `libstdc++`. You can use `up` (see [Selection](Selection.html#Selection)) to get to your code.
-   If you call a function interactively, [GDB] is listening for, or exits. This is the case even if you set a catchpoint for the exception; catchpoints on exceptions are disabled within interactive calls. See [Calling](Calling.html#Calling), for information on controlling this with `set unwind-on-terminating-exception`.
-   You cannot raise an exception interactively.
-   You cannot install an exception handler interactively.
```

`exception [name]`

:

```
An Ada exception being raised. If an exception name is specified at the end of the command (eg `catch exception Program_Error`), the debugger will stop only when this specific exception is raised. Otherwise, the debugger stops execution when any Ada exception is raised.

When inserting an exception catchpoint on a user-defined exception whose name is identical to one of the exceptions defined by the language, the fully qualified name must be used as the exception name. Otherwise, [GDB].



The convenience variable `$_ada_exception` holds the address of the exception being thrown. This can be useful when setting a condition for such a catchpoint.
```

`exception unhandled`

:

```
An exception that was raised but is not handled by the program. The convenience variable `$_ada_exception` is set as for `catch exception`.
```

`handlers [name]`

:

```
An Ada exception being handled. If an exception name is specified at the end of the command (eg [catch handlers Program_Error]), the debugger will stop only when this specific exception is handled. Otherwise, the debugger stops execution when any Ada exception is handled.

When inserting a handlers catchpoint on a user-defined exception whose name is identical to one of the exceptions defined by the language, the fully qualified name must be used as the exception name. Otherwise, [GDB].

The convenience variable `$_ada_exception` is set as for `catch exception`.
```

`assert`

:

```
A failed Ada assertion. Note that the convenience variable `$_ada_exception` is *not* set by this catchpoint.
```

`exec`

:

```
A call to `exec`.


```

`syscall`
`syscall [name | number | group:groupname | g:groupname] …`

:

```
A call to or return from a system call, a.k.a. *syscall*. A syscall is a mechanism for application programs to request a service from the operating system (OS) or one of the OS system services. [GDB] can catch some or all of the syscalls issued by the debuggee, and show the related information for each syscall. If no argument is specified, calls to and returns from all system calls will be caught.

`name`.

Normally, [GDB] command-line completion facilities (see [command completion](Completion.html#Completion)) to list the available choices.

You may also specify the system call numerically. A syscall's number is the value passed to the OS's syscall dispatcher to identify the requested service. When you specify the syscall by its name, [GDB] lags behind the OS upgrades).

You may specify a group of related syscalls to be caught at once using the `group:` syntax (`g:` is a shorter equivalent). For instance, on some platforms [GDB] allows you to catch all network related syscalls, by passing the argument `group:network` to `catch syscall`. Note that not all syscall groups are available in every system. You can use the command completion facilities (see [command completion](Completion.html#Completion)) to list the syscall groups available on your environment.

The example below illustrates how this command works if you don't provide arguments to it:

::: smallexample
``` smallexample
(gdb) catch syscall
Catchpoint 1 (syscall)
(gdb) r

Starting program: /tmp/catch-syscall

> 开始程序：/tmp/catch-syscall


Catchpoint 1 (call to syscall 'close'), \

> 捕获点1（调用系统调用“关闭”）
       0xffffe424 in __kernel_vsyscall ()
(gdb) c
Continuing.


Catchpoint 1 (returned from syscall 'close'), \

> 捕获点1（从系统调用“close”返回）
    0xffffe424 in __kernel_vsyscall ()
(gdb)
```

:::

Here is an example of catching a system call by name:

::: smallexample

```bash

(gdb) catch syscall chroot

> (gdb) 捕获系统调用 chroot

Catchpoint 1 (syscall 'chroot' [61])

> 捕获点1（系统调用“chroot”[61]）
(gdb) r

Starting program: /tmp/catch-syscall

> 开始程序：/tmp/catch-syscall


Catchpoint 1 (call to syscall 'chroot'), \

> 捕获点1（调用系统调用'chroot'）
           0xffffe424 in __kernel_vsyscall ()
(gdb) c
Continuing.


Catchpoint 1 (returned from syscall 'chroot'), \

> 捕获点1（从系统调用“chroot”返回）
    0xffffe424 in __kernel_vsyscall ()
(gdb)
```

:::

An example of specifying a system call numerically. In the case below, the syscall number has a corresponding entry in the XML file, so [GDB] finds its name and prints it:

::: smallexample

```bash
(gdb) catch syscall 252

Catchpoint 1 (syscall(s) 'exit_group')

> 捕获点1（系统调用'sexit_group'）
(gdb) r

Starting program: /tmp/catch-syscall

> 开始程序：/tmp/catch-syscall


Catchpoint 1 (call to syscall 'exit_group'), \

> 捕获点1（调用系统调用“exit_group”）
           0xffffe424 in __kernel_vsyscall ()
(gdb) c
Continuing.


Program exited normally.

> 程序正常退出。
(gdb)
```

:::

Here is an example of catching a syscall group:

::: smallexample

```bash

(gdb) catch syscall group:process

> (gdb) 捕获系统调用组: 处理

Catchpoint 1 (syscalls 'exit' [1] 'fork' [2] 'waitpid' [7]

> 捕获点1（系统调用'exit'[1] 'fork'[2] 'waitpid'[7]）

'execve' [11] 'wait4' [114] 'clone' [120] 'vfork' [190]

> 'execve' [11]：执行  'wait4' [114]：等待4  'clone' [120]：克隆  'vfork' [190]：vfork

'exit_group' [252] 'waitid' [284] 'unshare' [310])

> 退出组[252]等待[284]不共享[310]
(gdb) r

Starting program: /tmp/catch-syscall

> 开始程序：/tmp/catch-syscall


Catchpoint 1 (call to syscall fork), 0x00007ffff7df4e27 in open64 ()

> 捕获点1（调用系统调用fork），在open64（）中的0x00007ffff7df4e27。

   from /lib64/ld-linux-x86-64.so.2

> 从/lib64/ld-linux-x86-64.so.2

(gdb) c
Continuing.
```

:::

However, there can be situations when there is no corresponding name in XML file for that syscall number. In this case, [GDB] prints a warning message saying that it was not able to find the syscall name, but the catchpoint will be set anyway. See the example below:

::: smallexample

```bash
(gdb) catch syscall 764

warning: The number '764' does not represent a known syscall.

> 警告：数字“764”不代表一个已知的系统调用。

Catchpoint 2 (syscall 764)

> 捕获点2（系统调用764）
(gdb)
```

:::

If you configure [GDB]' option, it will not be able to display syscall names. Also, if your architecture does not have an XML file describing its system calls, you will not be able to see the syscall names. It is important to notice that these two features are used for accessing the syscall name database. In either case, you will see a warning like this:

::: smallexample

```bash
(gdb) catch syscall

warning: Could not open "syscalls/i386-linux.xml"

> 警告：无法打开“syscalls/i386-linux.xml”

warning: Could not load the syscall XML file 'syscalls/i386-linux.xml'.

> 警告：无法加载系统调用XML文件'syscalls/i386-linux.xml'。

GDB will not be able to display syscall names.

> GDB无法显示系统调用的名称。
Catchpoint 1 (syscall)
(gdb)
```

:::

Of course, the file name will change depending on your architecture and system.

Still using the example above, you can also try to catch a syscall by its number. In this case, you would see something like:

::: smallexample

```bash
(gdb) catch syscall 252

Catchpoint 1 (syscall(s) 252)

> 捕获点1（系统调用（s）252）
```

:::

Again, in this case [GDB] would not be able to display syscall's names.

```

`fork`

:   

```

A call to `fork`.

```

`vfork`

:   

```

A call to `vfork`.

```

`load [regexp]`
`unload [regexp]`

:   

```

The loading or unloading of a shared library. If `regexp` is given, then the catchpoint will stop only if the regular expression matches one of the affected libraries.

```

`signal [signal… | ‘all’]`

:   

```

The delivery of a signal.

With no arguments, this catchpoint will catch any signal that is not used internally by [GDB]'.

With the argument '`all`, will be caught. This argument cannot be used with other signal names.

Otherwise, the arguments are a list of signal names as given to `handle` (see [Signals](Signals.html#Signals)). Only signals specified in this list will be caught.

One reason that `catch signal` can be more useful than `handle` is that you can attach commands and conditions to the catchpoint.

When a signal is caught by a catchpoint, the signal's `stop` and `print` settings, as specified by `handle`, are ignored. However, whether the signal is still delivered to the inferior depends on the `pass` setting; this can be changed in the catchpoint's commands.

```

`tcatch event`




Set a catchpoint that is enabled only for one stop. The catchpoint is automatically deleted after the first time the event is caught.

> 设置一个仅在一次停止时启用的捕获点。第一次捕获事件后，该捕获点将自动删除。


Use the `info break` command to list the current catchpoints.

> 使用`info break`命令列出当前的捕获点。

---

::: header
Next: [Delete Breaks](Delete-Breaks.html#Delete-Breaks)]
:::
```
