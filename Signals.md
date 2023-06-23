---
tip: translate by openai@2023-06-23 13:16:46
...
---
description: Signals (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Signals (Debugging with GDB)
lang: en
resource-type: document
title: Signals (Debugging with GDB)
---
::: header
Next: [Thread Stops](Thread-Stops.html#Thread-Stops)]
:::

---

### 5.4 Signals


A signal is an asynchronous event that can happen in a program. The operating system defines the possible kinds of signals, and gives each kind a name and a number. For example, in Unix `SIGINT` is the signal a program gets when you type an interrupt character (often [Ctrl-c]); `SIGSEGV` is the signal a program gets from referencing a place in memory far away from all the areas in use; `SIGALRM` occurs when the alarm clock timer goes off (which happens only if your program has requested an alarm).

> 信号是程序中可能发生的异步事件。操作系统定义了可能的信号类型，并为每种类型赋予一个名称和编号。例如，在Unix中，当您键入中断字符（通常是[Ctrl-c]）时，程序将收到SIGINT信号；当程序引用远离所有使用区域的内存位置时，将收到SIGSEGV信号；如果程序请求设置警报，则会发生SIGALRM信号。


Some signals, including `SIGALRM`, are a normal part of the functioning of your program. Others, such as `SIGSEGV`, indicate errors; these signals are *fatal* (they kill your program immediately) if the program has not specified in advance some other way to handle the signal. `SIGINT` does not indicate an error in your program, but it is normally fatal so it can carry out the purpose of the interrupt: to kill the program.

> 一些信号，包括`SIGALRM`，是程序正常运行的一部分。其他的，如`SIGSEGV`，表示错误；如果程序没有提前指定如何处理这些信号，这些信号将是*致命的*（它们会立即杀死程序）。`SIGINT`不表示程序中的错误，但它通常是致命的，因此它可以完成中断的目的：杀死程序。


[GDB] in advance what to do for each kind of signal.

> [GDB] 提前了解每种信号需要做什么。


Normally, [GDB] is set up to let the non-erroneous signals like `SIGALRM` be silently passed to your program (so as not to interfere with their role in the program's functioning) but to stop your program immediately whenever an error signal happens. You can change these settings with the `handle` command.

> 一般来说，GDB被设置为让像SIGALRM这样的非错误信号被静默地传递给您的程序（以免干扰程序运行），但是一旦发生错误信号，就会立即停止您的程序。您可以使用handle命令更改这些设置。

`info signals`

`info handle`


Print a table of all the kinds of signals and how [GDB] has been told to handle each one. You can use this to see the signal numbers of all the defined types of signals.

> 打印出所有类型信号以及[GDB] 如何处理它们的表格。您可以使用这个表格查看所有定义的类型信号的信号号码。

`info signals sig`


Similar, but print information only about the specified signal number.

> 打印指定信号号码的信息。

`info handle` is an alias for `info signals`.

`catch signal [signal… | ‘all’]`


Set a catchpoint for the indicated signals. See [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints), for details about this command.

> 设置指定信号的捕获点。有关此命令的详细信息，请参阅[设置捕获点](Set-Catchpoints.html#Set-Catchpoints)。

`handle signal [ signal … ] [keywords…]`


Change the way [GDB], described below, say what changes to make to all of the specified signals.

> 更改下面描述的GDB，说明对所有指定信号所做的更改。


The keywords allowed by the `handle` command can be abbreviated. Their full names are:

> 命令“handle”允许的关键字可以缩写。它们的完整名称是：

`nostop`


:   [GDB] should not stop your program when this signal happens. It may still print a message telling you that the signal has come in.

> GDB不应该在这个信号发生时停止您的程序。它仍然可能会打印一条消息告诉您信号已经到达。

`stop`


:   [GDB] should stop your program when this signal happens. This implies the `print` keyword as well.

> GDB 应在此信号发生时停止您的程序。这也意味着使用 `print` 关键字。

`print`


:   [GDB] should print a message when this signal happens.

> GDB应该在这个信号发生时打印一条消息。

`noprint`


:   [GDB] should not mention the occurrence of the signal at all. This implies the `nostop` keyword as well.

> GDB不應該提及信號的發生，這也意味著必須使用`nostop`關鍵字。

`pass`
`noignore`


:   [GDB] should allow your program to see this signal; your program can handle the signal, or else it may terminate if the signal is fatal and not handled. `pass` and `noignore` are synonyms.

> GDB应允许您的程序看到这个信号；您的程序可以处理信号，否则如果信号是致命的而且没有被处理，它可能会终止。`pass`和`noignore`是同义词。

`nopass`
`ignore`


:   [GDB] should not allow your program to see this signal. `nopass` and `ignore` are synonyms.

> GDB不应该允许你的程序看到这个信号。`nopass`和`ignore`是同义词。


When a signal stops your program, the signal is not visible to the program until you continue. Your program sees the signal then, if `pass` is in effect for the signal in question *at that time*. In other words, after [GDB] reports a signal, you can use the `handle` command with `pass` or `nopass` to control whether your program sees that signal when you continue.

> 当一个信号停止你的程序时，该信号对程序不可见，直到你继续。你的程序在那时会看到信号，如果该信号在那个时候有效。换句话说，当[GDB]报告一个信号后，你可以使用`handle`命令和`pass`或`nopass`来控制你的程序在你继续时是否看到该信号。


The default is set to `nostop`, `noprint`, `pass` for non-erroneous signals such as `SIGALRM`, `SIGWINCH` and `SIGCHLD`, and to `stop`, `print`, `pass` for the erroneous signals.

> 默认设置为非错误信号（如SIGALRM、SIGWINCH和SIGCHLD）的nostop、noprint、pass，而错误信号的设置则为stop、print、pass。


You can also use the `signal` command to prevent your program from seeing a signal, or cause it to see a signal it normally would not see, or to give it any signal at any time. For example, if your program stopped due to some sort of memory reference error, you might store correct values into the erroneous variables and continue, hoping to see more execution; but your program would probably terminate immediately as a result of the fatal signal once it saw the signal. To prevent this, you can continue with '`signal 0`'. See [Giving your Program a Signal](Signaling.html#Signaling).

> 你也可以使用`signal`命令来阻止程序看到一个信号，或使它看到它通常不会看到的信号，或在任何时候给它任何信号。例如，如果您的程序由于某种内存引用错误而停止，您可能会将正确的值存储到错误的变量中，然后继续，希望看到更多的执行；但是一旦它看到信号，您的程序可能会立即因致命信号而终止。为了防止这种情况，您可以使用`signal 0`继续。请参阅[给程序发信号](Signaling.html#Signaling)。


[GDB] still informs you that the program received a signal if `handle print` is set.

> 如果设置了`handle print`，GDB 仍然会告知程序收到了一个信号。


If you set `handle pass` for a signal, and your program sets up a handler for it, then issuing a stepping command, such as `step` or `stepi`, when your program is stopped due to the signal will step *into* the signal handler (if the target supports that).

> 如果你为一个信号设置了“处理传递”，而你的程序设置了一个处理程序，那么当你的程序由于信号而停止时，发出一个步进命令（如`step`或`stepi`），将会步入信号处理程序（如果目标支持的话）。


Likewise, if you use the `queue-signal` command to queue a signal to be delivered to the current thread when execution of the thread resumes (see [Giving your Program a Signal](Signaling.html#Signaling)), then a stepping command will step into the signal handler.

> 同样，如果您使用`queue-signal`命令将信号排队以在线程恢复执行时发送到当前线程（参见[给你的程序一个信号]（Signaling.html#Signaling）），那么跳步命令将跳入信号处理程序。


Here's an example, using `stepi` to step to the first instruction of `SIGUSR1`'s handler:

> 以下是一个例子，使用`stepi`跳转到`SIGUSR1`处理程序的第一条指令：

::: smallexample

```bash
(gdb) handle SIGUSR1
Signal        Stop      Print   Pass to program Description
SIGUSR1       Yes       Yes     Yes             User defined signal 1
(gdb) c
Continuing.

Program received signal SIGUSR1, User defined signal 1.
main () sigusr1.c:28
28        p = 0;
(gdb) si
sigusr1_handler () at sigusr1.c:9
9       {
```

:::


The same, but using `queue-signal` instead of waiting for the program to receive the signal first:

> 使用`queue-signal`而不是等待程序首先接收信号，情况也是一样的。

::: smallexample

```bash
(gdb) n
28        p = 0;
(gdb) queue-signal SIGUSR1
(gdb) si
sigusr1_handler () at sigusr1.c:9
9       {
(gdb)
```

:::


On some targets, [GDB] system header.

> 在一些目标上，[GDB]系统头文件。


Here's an example, on a [GNU]/Linux system, printing the stray referenced address that raised a segmentation fault.

> 这是一个例子，在[GNU]/Linux系统上，打印出引发段错误的无效地址。

::: smallexample

```bash
(gdb) continue
Program received signal SIGSEGV, Segmentation fault.
0x0000000000400766 in main ()
69        *(int *)p = 0;
(gdb) ptype $_siginfo
type = struct {
    int si_signo;
    int si_errno;
    int si_code;
    union {
        int _pad[28];
        struct  _kill;
        struct  _timer;
        struct  _rt;
        struct  _sigchld;
        struct  _sigfault;
        struct  _sigpoll;
    } _sifields;
}
(gdb) ptype $_siginfo._sifields._sigfault
type = struct {
    void *si_addr;
}
(gdb) p $_siginfo._sifields._sigfault.si_addr
$1 = (void *) 0x7ffff7ff7000
```

:::


Depending on target support, `$_siginfo` may also be writable.

> 根据目标支持，`$_siginfo`也可能可写。


On some targets, a `SIGSEGV` can be caused by a boundary violation, i.e., accessing an address outside of the allowed range. In those cases [GDB] displays the violation kind: \"Upper\" or \"Lower\", the memory address accessed and the bounds, while with `handle nostop SIGSEGV` no additional information is displayed.

> 在某些目标上，`SIGSEGV`可能是由边界违规引起的，即访问超出允许范围的地址。在这种情况下，[GDB]会显示违规类型：“Upper”或“Lower”，访问的内存地址以及边界，而使用`handle nostop SIGSEGV`则不会显示额外的信息。


The usual output of a segfault is:

> 通常的段错误输出是：

::: smallexample

```bash
Program received signal SIGSEGV, Segmentation fault
0x0000000000400d7c in upper () at i386-mpx-sigsegv.c:68
68        value = *(p + len);
```

:::


While a bound violation is presented as:

> 当出现约束违规时：

::: smallexample

```bash
Program received signal SIGSEGV, Segmentation fault
Upper bound violation while accessing address 0x7fffffffc3b3
Bounds: [lower = 0x7fffffffc390, upper = 0x7fffffffc3a3]
0x0000000000400d7c in upper () at i386-mpx-sigsegv.c:68
68        value = *(p + len);
```

:::

---

::: header
Next: [Thread Stops](Thread-Stops.html#Thread-Stops)]
:::
