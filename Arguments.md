---
tip: translate by openai@2023-06-23 17:26:21
...
---
description: Arguments (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Arguments (Debugging with GDB)
lang: en
resource-type: document
title: Arguments (Debugging with GDB)
---
::: header
Next: [Environment](Environment.html#Environment)]
:::

---

### 4.3 Your Program's Arguments


The arguments to your program can be specified by the arguments of the `run` command. They are passed to a shell, which expands wildcard characters and performs redirection of I/O, and thence to your program. Your `SHELL` environment variable (if it exists) specifies what shell [GDB] on Unix).

> 程序的参数可以通过`run`命令的参数指定。它们会被传递给一个shell，它会展开通配符字符并执行输入/输出重定向，然后传递给您的程序。您的`SHELL`环境变量（如果存在）指定了在Unix上的GDB使用的shell是什么。


On non-Unix systems, the program is usually invoked directly by [GDB], which emulates I/O redirection via the appropriate system calls, and the wildcard characters are expanded by the startup code of the program, not by the shell.

> 在非Unix系统上，该程序通常由GDB直接调用，GDB通过适当的系统调用模拟I/O重定向，通配符由程序的启动代码而不是shell展开。

`run` with no arguments uses the same arguments used by the previous `run`, or those set by the `set args` command.

`set args`


Specify the arguments to be used the next time your program is run. If `set args` has no arguments, `run` executes your program with no arguments. Once you have run your program with arguments, using `set args` before the next `run` is the only way to run it again without arguments.

> 下次运行程序时使用的参数，请使用`set args`指定。如果`set args`没有参数，`run`就会没有参数地执行程序。一旦你用参数运行了程序，在下次`run`之前使用`set args`是唯一的方法，可以不使用参数重新运行程序。

`show args`


Show the arguments to give your program when it is started.

> 显示当程序启动时要给它的参数。
