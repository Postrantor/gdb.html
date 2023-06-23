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

Some signals, including `SIGALRM`, are a normal part of the functioning of your program. Others, such as `SIGSEGV`, indicate errors; these signals are *fatal* (they kill your program immediately) if the program has not specified in advance some other way to handle the signal. `SIGINT` does not indicate an error in your program, but it is normally fatal so it can carry out the purpose of the interrupt: to kill the program.

[GDB] in advance what to do for each kind of signal.

Normally, [GDB] is set up to let the non-erroneous signals like `SIGALRM` be silently passed to your program (so as not to interfere with their role in the program's functioning) but to stop your program immediately whenever an error signal happens. You can change these settings with the `handle` command.

`info signals`

`info handle`

Print a table of all the kinds of signals and how [GDB] has been told to handle each one. You can use this to see the signal numbers of all the defined types of signals.

`info signals sig`

Similar, but print information only about the specified signal number.

`info handle` is an alias for `info signals`.

`catch signal [signal… | ‘all’]`

Set a catchpoint for the indicated signals. See [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints), for details about this command.

`handle signal [ signal … ] [keywords…]`

Change the way [GDB], described below, say what changes to make to all of the specified signals.

The keywords allowed by the `handle` command can be abbreviated. Their full names are:

`nostop`

:   [GDB] should not stop your program when this signal happens. It may still print a message telling you that the signal has come in.

`stop`

:   [GDB] should stop your program when this signal happens. This implies the `print` keyword as well.

`print`

:   [GDB] should print a message when this signal happens.

`noprint`

:   [GDB] should not mention the occurrence of the signal at all. This implies the `nostop` keyword as well.

`pass`
`noignore`

:   [GDB] should allow your program to see this signal; your program can handle the signal, or else it may terminate if the signal is fatal and not handled. `pass` and `noignore` are synonyms.

`nopass`
`ignore`

:   [GDB] should not allow your program to see this signal. `nopass` and `ignore` are synonyms.

When a signal stops your program, the signal is not visible to the program until you continue. Your program sees the signal then, if `pass` is in effect for the signal in question *at that time*. In other words, after [GDB] reports a signal, you can use the `handle` command with `pass` or `nopass` to control whether your program sees that signal when you continue.

The default is set to `nostop`, `noprint`, `pass` for non-erroneous signals such as `SIGALRM`, `SIGWINCH` and `SIGCHLD`, and to `stop`, `print`, `pass` for the erroneous signals.

You can also use the `signal` command to prevent your program from seeing a signal, or cause it to see a signal it normally would not see, or to give it any signal at any time. For example, if your program stopped due to some sort of memory reference error, you might store correct values into the erroneous variables and continue, hoping to see more execution; but your program would probably terminate immediately as a result of the fatal signal once it saw the signal. To prevent this, you can continue with '`signal 0`'. See [Giving your Program a Signal](Signaling.html#Signaling).

[GDB] still informs you that the program received a signal if `handle print` is set.

If you set `handle pass` for a signal, and your program sets up a handler for it, then issuing a stepping command, such as `step` or `stepi`, when your program is stopped due to the signal will step *into* the signal handler (if the target supports that).

Likewise, if you use the `queue-signal` command to queue a signal to be delivered to the current thread when execution of the thread resumes (see [Giving your Program a Signal](Signaling.html#Signaling)), then a stepping command will step into the signal handler.

Here's an example, using `stepi` to step to the first instruction of `SIGUSR1`'s handler:

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
