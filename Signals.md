---
tip: translate by openai@2023-06-24 02:56:53
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

> 信号是一种可以在程序中发生的异步事件。操作系统定义了可能出现的信号类型，并为每种类型赋予名称和编号。例如，在Unix系统中，当您键入中断字符（通常为[Ctrl-c]）时，程序会收到SIGINT信号；当程序引用远离所有使用区域的内存位置时，它会收到SIGSEGV信号；当闹钟定时器触发时（只有当程序请求设置闹钟时才会发生），SIGALRM信号会发生。


Some signals, including `SIGALRM`, are a normal part of the functioning of your program. Others, such as `SIGSEGV`, indicate errors; these signals are *fatal* (they kill your program immediately) if the program has not specified in advance some other way to handle the signal. `SIGINT` does not indicate an error in your program, but it is normally fatal so it can carry out the purpose of the interrupt: to kill the program.

> 一些信号，包括`SIGALRM`，是程序正常运行的一部分。其他的，如`SIGSEGV`，指示错误；如果程序没有提前指定其他的处理方式，这些信号是致命的（它们会立即杀死你的程序）。`SIGINT`并不指示程序中的错误，但通常是致命的，因此它可以执行中断的目的：杀死程序。

[GDB] in advance what to do for each kind of signal.


Normally, [GDB] is set up to let the non-erroneous signals like `SIGALRM` be silently passed to your program (so as not to interfere with their role in the program's functioning) but to stop your program immediately whenever an error signal happens. You can change these settings with the `handle` command.

> 一般来说，[GDB]被设置为让像`SIGALRM`这样的非错误信号被静默地传递到您的程序（以免干扰程序的功能），但是当发生错误信号时立即停止您的程序。您可以使用`handle`命令更改这些设置。

`info signals`

`info handle`


Print a table of all the kinds of signals and how [GDB] has been told to handle each one. You can use this to see the signal numbers of all the defined types of signals.

> 打印出所有信号类型及[GDB]如何处理它们的表格。您可以使用它来查看所有定义的信号类型的信号编号。

`info signals sig`

Similar, but print information only about the specified signal number.

`info handle` is an alias for `info signals`.

`catch signal [signal… | ‘all’]`


Set a catchpoint for the indicated signals. See [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints), for details about this command.

> 设置指定信号的捕获点。有关该命令的详细信息，请参阅[Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)。

`handle signal [ signal … ] [keywords…]`


Change the way [GDB], described below, say what changes to make to all of the specified signals.

> 改变下面描述的GDB的方式，对所有指定的信号做出更改。


The keywords allowed by the `handle` command can be abbreviated. Their full names are:

> 命令`handle`允许的关键字可以缩写。它们的完整名称是：

`nostop`


:   [GDB] should not stop your program when this signal happens. It may still print a message telling you that the signal has come in.

> GDB不应该在这个信号发生时停止你的程序，它可能仍会打印一条消息提示你这个信号已经发生。

`stop`


:   [GDB] should stop your program when this signal happens. This implies the `print` keyword as well.

> GDB应该在发生这个信号时停止你的程序。这也意味着使用`print`关键字。

`print`

:   [GDB] should print a message when this signal happens.

`noprint`


:   [GDB] should not mention the occurrence of the signal at all. This implies the `nostop` keyword as well.

> GDB不应提及信号的发生，这也意味着要使用`nostop`关键字。

`pass`
`noignore`


:   [GDB] should allow your program to see this signal; your program can handle the signal, or else it may terminate if the signal is fatal and not handled. `pass` and `noignore` are synonyms.

> GDB 应该允许你的程序看到这个信号; 你的程序可以处理这个信号，否则如果信号是致命的并且没有处理，它可能会终止。`pass`和`noignore`是同义词。

`nopass`
`ignore`


:   [GDB] should not allow your program to see this signal. `nopass` and `ignore` are synonyms.

> GDB不应该允许你的程序看到这个信号。`nopass`和`ignore`是同义词。


When a signal stops your program, the signal is not visible to the program until you continue. Your program sees the signal then, if `pass` is in effect for the signal in question *at that time*. In other words, after [GDB] reports a signal, you can use the `handle` command with `pass` or `nopass` to control whether your program sees that signal when you continue.

> 当一个信号停止你的程序时，在你继续之前，这个信号对程序不可见。当你继续时，你的程序就会看到这个信号，如果此时该信号的处理方式为`pass`。换句话说，在[GDB]报告一个信号后，你可以使用`handle`命令带上`pass`或`nopass`来控制你的程序在你继续时是否看到该信号。


The default is set to `nostop`, `noprint`, `pass` for non-erroneous signals such as `SIGALRM`, `SIGWINCH` and `SIGCHLD`, and to `stop`, `print`, `pass` for the erroneous signals.

> 默认设置为对于非错误信号（如SIGALRM、SIGWINCH和SIGCHLD），设置为nostop、noprint、pass，对于错误信号设置为stop、print、pass。


You can also use the `signal` command to prevent your program from seeing a signal, or cause it to see a signal it normally would not see, or to give it any signal at any time. For example, if your program stopped due to some sort of memory reference error, you might store correct values into the erroneous variables and continue, hoping to see more execution; but your program would probably terminate immediately as a result of the fatal signal once it saw the signal. To prevent this, you can continue with '`signal 0`'. See [Giving your Program a Signal](Signaling.html#Signaling).

> 你也可以使用`signal`命令来防止程序看到一个信号，或使它看到一个通常不会看到的信号，或在任何时候给它任何信号。例如，如果你的程序由于某种内存引用错误而停止，你可能会将正确的值存储到错误的变量中并继续执行，希望看到更多的执行；但是一旦它看到信号，你的程序可能会立即因致命信号而终止。为了防止这种情况，你可以继续使用'`signal 0`'。请参阅[给你的程序一个信号](Signaling.html#Signaling)。


[GDB] still informs you that the program received a signal if `handle print` is set.

> GDB仍然会告知程序收到信号，如果`handle print`被设置。


If you set `handle pass` for a signal, and your program sets up a handler for it, then issuing a stepping command, such as `step` or `stepi`, when your program is stopped due to the signal will step *into* the signal handler (if the target supports that).

> 如果您为信号设置了“处理传递”，并且您的程序为其设置了处理程序，那么在由于信号而停止您的程序时，发出步进命令（例如“步进”或“步进”）将步入信号处理程序（如果目标支持）。


Likewise, if you use the `queue-signal` command to queue a signal to be delivered to the current thread when execution of the thread resumes (see [Giving your Program a Signal](Signaling.html#Signaling)), then a stepping command will step into the signal handler.

> 如果您使用`queue-signal`命令将信号排队发送到当前线程（参见[给程序发送信号](Signaling.html#Signaling)），当线程恢复执行时，步进命令将步入信号处理程序。


Here's an example, using `stepi` to step to the first instruction of `SIGUSR1`'s handler:

> 这是一个使用`stepi`跳转到`SIGUSR1`处理程序的第一条指令的例子：

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


Here's an example, on a [GNU]/Linux system, printing the stray referenced address that raised a segmentation fault.

> 在[GNU]/Linux系统上，这是一个例子，打印出引发段错误的无关地址。

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


On some targets, a `SIGSEGV` can be caused by a boundary violation, i.e., accessing an address outside of the allowed range. In those cases [GDB] displays the violation kind: \"Upper\" or \"Lower\", the memory address accessed and the bounds, while with `handle nostop SIGSEGV` no additional information is displayed.

> 在某些目标上，`SIGSEGV`可能由边界违规引起，即访问超出允许范围的地址。在这种情况下，[GDB]显示违规类型：“Upper”或“Lower”，访问的内存地址以及边界，而使用`handle nostop SIGSEGV`则不显示任何附加信息。

The usual output of a segfault is:

::: smallexample

```bash
Program received signal SIGSEGV, Segmentation fault
0x0000000000400d7c in upper () at i386-mpx-sigsegv.c:68
68        value = *(p + len);
```

:::

While a bound violation is presented as:

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
