---
tip: translate by openai@2023-06-23 13:38:05
...
---
description: Stop Reply Packets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Stop Reply Packets (Debugging with GDB)
lang: en
resource-type: document
title: Stop Reply Packets (Debugging with GDB)
---
::: header
Next: [General Query Packets](General-Query-Packets.html#General-Query-Packets)]
:::

---

### E.3 Stop Reply Packets

The '`C` source code.


In non-stop mode, the server will simply reply '`OK`'; any stop will be the subject of a future notification. See [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop).

> 在非停止模式下，服务器将简单地回复'OK'；任何停止将成为未来通知的主题。请参阅[远程非停止](Remote-Non_002dStop.html#Remote-Non_002dStop)。


As in the description of request packets, we include spaces in the reply templates for clarity; these are not part of the reply packet's syntax. No [GDB] stop reply packet uses spaces to separate its components.

> 按照请求数据包的描述，我们在回复模板中包含空格以提高可读性；这些不是回复数据包语法的一部分。没有[GDB]停止回复数据包使用空格来分隔其组件。

'`S AA`'


:   The program received signal number `AA` pairs.

> 程序收到了AA对的信号。

'`T AA n1:r1;n2:r2;…`'

:

```
The program received signal number `AA`' pair is interpreted as follows:

-   If `n` is a series of bytes in target byte order, with each byte given by a two-digit hex number.
-   If `n` is the thread ID of the stopped thread, as specified in [thread-id syntax](Packets.html#thread_002did-syntax).
-   If `n` is the hexadecimal number of the core on which the stop event was detected.
-   If `n`', the trap signal. At most one stop reason should be present.
-   Otherwise, [GDB]' pair and go on to the next; this allows us to extend the protocol in the future.

The currently defined stop reasons are:

'`watch`'\
'`rwatch`'\
'`awatch`'

:   The packet indicates a watchpoint hit, and `r` is the data address, in hex.

'`syscall_entry`'\
'`syscall_return`'

:   The packet indicates a syscall entry or return, and `r` is the syscall number, in hex.

    

'`library`'

:   The packet indicates that the loaded libraries have changed. [GDB] part is ignored.

    

'`replaylog`'

:   The packet indicates that the target cannot continue replaying logged execution events, because it has reached the end (or the beginning when executing backward) of the log. The value of `r`'. See [Reverse Execution](Reverse-Execution.html#Reverse-Execution), for more information.

'`swbreak`'

:   

    The packet indicates a software breakpoint instruction was executed, irrespective of whether it was [GDB] part must be left empty.

    On some architectures, such as x86, at the architecture level, when a breakpoint instruction executes the program counter points at the breakpoint address plus an offset. On such targets, the stub is responsible for adjusting the PC to point back at the breakpoint address.

    This packet should not be sent by default; older [GDB]' feature indicating support.

    This packet is required for correct non-stop mode operation.

'`hwbreak`'

:   The packet indicates the target stopped for a hardware breakpoint. The `r` part must be left empty.

    The same remarks about '`qSupported`' and non-stop mode above apply.

    

'`fork`'

:   The packet indicates that `fork` was called, and `r` is the thread ID of the new child process, as specified in [thread-id syntax](Packets.html#thread_002did-syntax). This packet is only applicable to targets that support fork events.

    This packet should not be sent by default; older [GDB]' feature indicating support.

    

'`vfork`'

:   The packet indicates that `vfork` was called, and `r` is the thread ID of the new child process, as specified in [thread-id syntax](Packets.html#thread_002did-syntax). This packet is only applicable to targets that support vfork events.

    This packet should not be sent by default; older [GDB]' feature indicating support.

    

'`vforkdone`'

:   The packet indicates that a child process created by a vfork has either called `exec` or terminated, so that the address spaces of the parent and child process are no longer shared. The `r` part is ignored. This packet is only applicable to targets that support vforkdone events.

    This packet should not be sent by default; older [GDB]' feature indicating support.

    

'`exec`'

:   The packet indicates that `execve` was called, and `r` is the absolute pathname of the file that was executed, in hex. This packet is only applicable to targets that support exec events.

    This packet should not be sent by default; older [GDB]' feature indicating support.

    

'`create`'

:   The packet indicates that the thread was just created. The new thread is stopped until [GDB] part is ignored.
```

'`W AA`'
'`W AA ; process:pid`'


:   The process exited, and `AA` is the exit status. This is only applicable to certain targets.

> 进程已退出，并且`AA`是退出状态。这只适用于某些目标。

```
The second form of the response, including the process ID of the exited process, can be used only when [GDB] are formatted as big-endian hex strings.
```

'`X AA`'
'`X AA ; process:pid`'


:   The process terminated with signal `AA`.

> 进程以信号“AA”终止。

```
The second form of the response, including the process ID of the terminated process, can be used only when [GDB] are formatted as big-endian hex strings.


```

'`w AA ; tid`'


:   The thread exited, and `AA` is formatted as a big-endian hex string.

> 线程已退出，AA被格式化为大端十六进制字符串。

'`N`'


:   There are no resumed threads left in the target. In other words, even though the process is alive, the last resumed thread has exited. For example, say the target process has two threads: thread 1 and thread 2. The client leaves thread 1 stopped, and resumes thread 2, which subsequently exits. At this point, even though the process is still alive, and thus no '`W`' feature indicating support.

> 在目标中没有剩余的恢复线程。换句话说，即使进程仍然存活，最后一个恢复的线程也已经退出。例如，假设目标进程有两个线程：线程1和线程2。客户端将线程1停止，并恢复线程2，后者随后退出。此时，即使进程仍然存活，也没有支持的“W”特性。

'`O XX…`'


:   '`XX…`', etc. This reply is not permitted in non-stop mode.

> 此回复在不间断模式下不允许。


'`F call-id,parameter…`'

> 'F call-id，参数...'


:   `call-id`. See [File-I/O Remote Protocol Extension](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension), for a list of implemented system calls.

> 调用ID。请参阅[文件I/O远程协议扩展](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension)，了解实现的系统调用列表。

```
'`parameter…`' is a list of parameters as defined for this very system call.

The target replies with this packet when it expects [GDB]' action is expected to be continued. See [File-I/O Remote Protocol Extension](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension), for more details.
```

---

::: header
Next: [General Query Packets](General-Query-Packets.html#General-Query-Packets)]
:::
