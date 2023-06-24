---
tip: translate by openai@2023-06-24 01:00:24
...
---
description: Packets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Packets (Debugging with GDB)
lang: en
resource-type: document
title: Packets (Debugging with GDB)
---
::: header
Next: [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets)]
:::

---

### E.2 Packets


The following table provides a complete list of all currently defined `command`. See [File-I/O Remote Protocol Extension](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension), for details about the File I/O extension of the remote protocol.

> 以下表格提供了当前定义的所有命令的完整列表。有关文件I/O远程协议扩展的详细信息，请参阅[File-I/O Remote Protocol Extension](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension)。


Each packet's description has a template showing the packet's overall syntax, followed by an explanation of the packet's meaning. We include spaces in some of the templates for clarity; these are not part of the packet's syntax. No [GDB].

> 每个数据包的描述都有一个模板，显示数据包的整体语法，然后解释数据包的含义。为了清晰起见，我们在一些模板中包含空格；这些不是数据包语法的一部分。没有[GDB]。

Several packets and replies include a `thread-id`' to pick any thread.


In addition, the remote protocol supports a multiprocess feature in which the `thread-id`.

> 此外，远程协议支持多进程功能，其中包括“线程ID”。


The multiprocess `thread-id`'. See [multiprocess extensions](General-Query-Packets.html#multiprocess-extensions), for more information.

> 多进程`thread-id`。有关更多信息，请参阅[多进程扩展](General-Query-Packets.html#multiprocess-extensions)。


Note that all packet forms beginning with an upper- or lower-case letter, other than those described here, are reserved for future use.

> 注意，除了这里描述的以大写或小写字母开头的数据包格式外，其他格式将保留供将来使用。

Here are the packet descriptions.

'`!`'

:

```
Enable extended mode. In extended mode, the remote server is made persistent. The '`R`' packet is used to restart the program being debugged.

Reply:

'`OK`'

:   The remote target both supports and has enabled extended mode.
```

'`?`'

:

```
This is sent when connection is first established to query the reason the target halted. The reply is the same as for step and continue. This packet has a special interpretation when the target is in non-stop mode; see [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop).

Reply: See [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets), for the reply specifications.
```

'`A arglen,argnum,arg,…`'

:

```
Initialized `argv` array passed into program. `arglen`. See `gdbserver` for more details.

Reply:

'`OK`'

:   The arguments were set.

'`E NN`'

:   An error occurred.
```

'`b baud`'

:

```
(Don't use this packet; its behavior is not well-defined.) Change the serial line speed to `baud`.

JTC: *When does the transport layer state change? When it's received, or after the ACK is transmitted. In either case, there are problems if the command or the acknowledgment packet is dropped.*

Stan: *If people really wanted to add something like this, and get it working for the first time, they ought to modify ser-unix.c to send some kind of out-of-band message to a specially-setup stub and have the switch happen \"in between\" packets, so that from remote protocol's point of view, nothing actually happened.*
```

'`B addr,mode`'

:

```
Set (`mode`.

Don't use this packet. Use the '`Z`' packets instead (see [insert breakpoint or watchpoint packet](#insert-breakpoint-or-watchpoint-packet)).


```

'`bc`'


:   Backward continue. Execute the target system in reverse. No parameter. See [Reverse Execution](Reverse-Execution.html#Reverse-Execution), for more information.

> 继续向后执行。反向执行目标系统，无需参数。更多信息请参见[反向执行](Reverse-Execution.html#Reverse-Execution)。

```
Reply: See [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets), for the reply specifications.


```

'`bs`'


:   Backward single step. Execute one instruction in reverse. No parameter. See [Reverse Execution](Reverse-Execution.html#Reverse-Execution), for more information.

> 逆向单步执行。反向执行一条指令。没有参数。更多信息请参阅[反向执行](Reverse-Execution.html#Reverse-Execution)。

```
Reply: See [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets), for the reply specifications.
```

'`c [addr]`'

:

```
Continue at `addr` is omitted, resume at current address.

This packet is deprecated for multi-threading support. See [vCont packet](#vCont-packet).

Reply: See [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets), for the reply specifications.
```

'`C sig[;addr]`'

:

```
Continue with signal `sig`' is omitted, resume at same address.

This packet is deprecated for multi-threading support. See [vCont packet](#vCont-packet).

Reply: See [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets), for the reply specifications.
```

'`d`'

:

```
Toggle debug flag.

Don't use this packet; instead, define a general set packet (see [General Query Packets](General-Query-Packets.html#General-Query-Packets)).
```

'`D`'
'`D;pid`'

:

```
The first form of the packet is used to detach [GDB] disconnects via the `detach` command.

The second form, including a process ID, is used when multiprocess protocol extensions are enabled (see [multiprocess extensions](General-Query-Packets.html#multiprocess-extensions)), to detach only a specific process. The `pid` is specified as a big-endian hex string.

Reply:

'`OK`'

:   for success

'`E NN`'

:   for an error
```

'`F RC,EE,CF;XX`'

:

```
A reply from [GDB]' packet sent by the target. This is part of the File-I/O protocol extension. See [File-I/O Remote Protocol Extension](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension), for the specification.
```

'`g`'

:

```
Read general registers.

Reply:

'`XX…`'

:   Each byte of register data is described by two hex digits. The bytes with the register are transmitted in target byte order. The size of each register and their position within the '`g`; typically this is some customary register layout for the architecture in question.

    When reading registers, the stub may also return a string of literal '`x`''s in place of the register data digits, to indicate that the corresponding register's value is unavailable. For example, when reading registers from a trace frame (see [Using the Collected Data](Analyze-Collected-Data.html#Analyze-Collected-Data)), this means that the register has not been collected in the trace frame. When reading registers from a live program, this indicates that the stub has no means to access the register contents, even though the corresponding register is known to exist. Note that if a register truly does not exist on the target, then it is better to not include it in the target description in the first place.

    For example, for an architecture with 4 registers of 4 bytes each, the following reply indicates to [GDB] that registers 0 and 2 are unavailable, while registers 1 and 3 are available, and both have zero value:

    ::: smallexample
    ``` smallexample
    -> g
    <- xxxxxxxx00000000xxxxxxxx00000000
    ```
    :::

'`E NN`'

:   for an error.
```

'`G XX…`'

:

```
Write general registers. See [read registers packet](#read-registers-packet), for a description of the `XX…` data.

Reply:

'`OK`'

:   for success

'`E NN`'

:   for an error
```

'`H op thread-id`'

:

```
Set thread for subsequent operations ('`m` has the format and interpretation described in [thread-id syntax](#thread_002did-syntax).

Reply:

'`OK`'

:   for success

'`E NN`'

:   for an error
```

'`i [addr[,nnn]]`'

:

```
Step the remote target by a single clock cycle. If '`,nnn` is present, cycle step starting at that address.
```

'`I`'

:

```
Signal, then cycle step. See [step with signal packet](#step-with-signal-packet). See [cycle step packet](#cycle-step-packet).
```

'`k`'

:

```
Kill request.

The exact effect of this packet is not specified.

For a bare-metal target, it may power cycle or reset the target system. For that reason, the '`k`' packet has no reply.

For a single-process target, it may kill that process if possible.

A multiple-process target may choose to kill just one process, or all that are under [GDB]'s control. For more precise control, use the vKill packet (see [vKill packet](#vKill-packet)).

If the target system immediately closes the connection in response to '`k` does not consider the lack of packet acknowledgment to be an error, and assumes the kill was successful.

If connected using [target extended-remote] probes the target state as if a new connection was opened (see [? packet](#g_t_003f-packet)).
```

'`m addr,length`'

:

```
Read `length` may not be aligned to any particular boundary.

The stub need not use any particular size or alignment when gathering data from memory for the response; even if `addr`

Reply:

'`XX…`'

:   Memory contents; each byte is transmitted as a two-digit hexadecimal number. The reply may contain fewer addressable memory units than requested if the server was able to read only part of the region of memory.

'`E NN`'

:   `NN` is errno
```

'`M addr,length:XX…`'

:

```
Write `length`; each byte is transmitted as a two-digit hexadecimal number.

Reply:

'`OK`'

:   for success

'`E NN`'

:   for an error (this includes the case where only part of the data was written).
```

'`p n`'

:

```
Read the value of register `n` is in hex. See [read registers packet](#read-registers-packet), for a description of how the returned register value is encoded.

Reply:

'`XX…`'

:   the register's value

'`E NN`'

:   for an error

'``'

:   Indicating an unrecognized `query`.
```

'`P n…=r…`'

:

```
Write register `n…` contains two hex digits for each byte in the register (target byte order).

Reply:

'`OK`'

:   for success

'`E NN`'

:   for an error
```

'`q name params…`'
'`Q name params…`'

:

```
General query ('`q`'). These packets are described fully in [General Query Packets](General-Query-Packets.html#General-Query-Packets).
```

'`r`'

:

```
Reset the entire system.

Don't use this packet; use the '`R`' packet instead.
```

'`R XX`'

:

```
Restart the program being debugged. The `XX`, while needed, is ignored. This packet is only available in extended mode (see [extended mode](#extended-mode)).

The '`R`' packet has no reply.
```

'`s [addr]`'

:

```
Single step, resuming at `addr` is omitted, resume at same address.

This packet is deprecated for multi-threading support. See [vCont packet](#vCont-packet).

Reply: See [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets), for the reply specifications.
```

'`S sig[;addr]`'

:

```
Step with signal. This is analogous to the '`C`' packet, but requests a single-step, rather than a normal resumption of execution.

This packet is deprecated for multi-threading support. See [vCont packet](#vCont-packet).

Reply: See [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets), for the reply specifications.
```

'`t addr:PP,MM`'

:

```
Search backwards starting at address `addr`.
```

'`T thread-id`'

:

```
Find out if the thread `thread-id` is alive. See [thread-id syntax](#thread_002did-syntax).

Reply:

'`OK`'

:   thread is still alive

'`E NN`'

:   thread is dead
```

'`v`'

:   Packets starting with '`v`' (or the end of the packet).

'`vAttach;pid`'

:

```
Attach to a new process with the specified process ID `pid`. The process ID is a hexadecimal integer identifying the process. In all-stop mode, all threads in the attached process are stopped; in non-stop mode, it may be attached without being stopped if that is supported by the target.

This packet is only available in extended mode (see [extended mode](#extended-mode)).

Reply:

'`E nn`'

:   for an error

'`Any stop packet`'

:   for success in all-stop mode (see [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets))

'`OK`'

:   for success in non-stop mode (see [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop))
```

'`vCont[;action[:thread-id]]…`'

:

```
Resume the inferior, specifying different actions for each thread.

For each inferior thread, the leftmost action with a matching `thread-id` matches all threads. Specifying no actions is an error.

Currently supported actions are:

'`c`'

:   Continue.

'`C sig`'

:   Continue with signal `sig` should be two hex digits.

'`s`'

:   Step.

'`S sig`'

:   Step with signal `sig` should be two hex digits.

'`t`'

:   Stop.

'`r start,end`'

:   Step once, and then keep stepping as long as the thread stops at addresses between `start` (exclusive). The remote stub reports a stop reply when either the thread goes out of the range or is stopped due to an unrelated reason, such as hitting a breakpoint. See [range stepping](Continuing-and-Stepping.html#range-stepping).

    If the range is empty (`start`).

    (A stop reply may be sent at any point even if the PC is still within the stepping range; for example, it is valid to implement this packet in a degenerate way as a single instruction step operation.)

The optional argument `addr`'.

The '`t`', regardless of whether the target uses some other signal as an implementation detail.

The server must ignore '`c`' actions for threads that are already stopped.

*Note:* In non-stop mode, a thread is considered running until [GDB]' packet (see [Remote Non-Stop](Remote-Non_002dStop.html#Remote-Non_002dStop)).

The stub must support '`vCont`' if it reports support for multiprocess extensions (see [multiprocess extensions](General-Query-Packets.html#multiprocess-extensions)).

Reply: See [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets), for the reply specifications.
```

'`vCont?`'

:

```
Request a list of actions supported by the '`vCont`' packet.

Reply:

'`vCont[;action…]`'

:   The '`vCont`' packet.

'``'

:   The '`vCont`' packet is not supported.


```

'`vCtrlC`'

:

```
Interrupt remote target as if a control-C was pressed on the remote terminal. This is the equivalent to reacting to the `^C` ('`\003`', the control-C character) character in all-stop mode while the target is running, except this works in non-stop mode. See [interrupting remote targets](Interrupts.html#interrupting-remote-targets), for more info on the all-stop variant.

Reply:

'`E nn`'

:   for an error

'`OK`'

:   for success
```

'`vFile:operation:parameter…`'

:

```
Perform a file operation on the target system. For details, see [Host I/O Packets](Host-I_002fO-Packets.html#Host-I_002fO-Packets).
```

'`vFlashErase:addr,length`'

:

```
Direct the stub to erase `length`' packet is received.

Reply:

'`OK`'

:   for success

'`E NN`'

:   for an error
```

'`vFlashWrite:addr:XX…`'

:

```
Direct the stub to write data to flash address `addr`' packet nor by some other target-specific method, the results are unpredictable.

Reply:

'`OK`'

:   for success

'`E.memtype`'

:   for vFlashWrite addressing non-flash memory

'`E NN`'

:   for an error
```

'`vFlashDone`'

:

```
Indicate to the stub that flash programming operation is finished. The stub is permitted to delay or batch the effects of a group of '`vFlashErase`' request is completed.
```

'`vKill;pid`'

:

```
Kill the process with the specified process ID `pid`' when multiprocess protocol extensions are supported; see [multiprocess extensions](General-Query-Packets.html#multiprocess-extensions).

Reply:

'`E nn`'

:   for an error

'`OK`'

:   for success
```

'`vMustReplyEmpty`'

:

```
The correct reply to an unknown '`v`' packets.

The '`vMustReplyEmpty`'.
```

'`vRun;filename[;argument]…`'

:

```
Run the program `filename` is an empty string, the stub may use a default program (e.g. the last program run). The program is created in the stopped state.

This packet is only available in extended mode (see [extended mode](#extended-mode)).

Reply:

'`E nn`'

:   for an error

'`Any stop packet`'

:   for success (see [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets))
```

'`vStopped`'

:

```
See [Notification Packets](Notification-Packets.html#Notification-Packets).
```

'`X addr,length:XX…`'

:

```
Write data to memory, where the data is transmitted in binary. Memory is specified by its address `addr`' is binary data (see [Binary Data](Overview.html#Binary-Data)).

Reply:

'`OK`'

:   for success

'`E NN`'

:   for an error
```

'`z type,addr,kind`'
'`Z type,addr,kind`'

:

```
Insert ('`Z`.

Each breakpoint and watchpoint packet `type` is documented separately.

*Implementation notes: A remote target shall return an empty string for an unrecognized breakpoint or watchpoint packet `type`' packet pair. To avoid potential problems with duplicate packets, the operations should be implemented in an idempotent way.*
```

'`z0,addr,kind`'
'`Z0,addr,kind[;cond_list…][;cmds:persist,cmd_list…]`'

:

```
Insert ('`Z0`.

A software breakpoint is implemented by replacing the instruction at `addr`.

See also the '`swbreak`.

The `cond_list` parameter is comprised of a series of expressions, concatenated without separators. Each expression has the following form:

'`X len,expr`'

:   `len` is the actual conditional expression in bytecode form.

The optional `cmd_list` disconnects from the target. Following this flag is a series of expressions concatenated with no separators. Each expression has the following form:

'`X len,expr`'

:   `len` is the actual commands expression in bytecode form.

*Implementation note: It is possible for a target to copy or move code that contains software breakpoints (e.g., when implementing overlays). The behavior of this packet, in the presence of such a target, is not defined.*

Reply:

'`OK`'

:   success

'``'

:   not supported

'`E NN`'

:   for an error
```

'`z1,addr,kind`'
'`Z1,addr,kind[;cond_list…][;cmds:persist,cmd_list…]`'

:

```
Insert ('`Z1`.

A hardware breakpoint is implemented using a mechanism that is not dependent on being able to modify the target's memory. The `kind`' packets.

*Implementation note: A hardware breakpoint is not affected by code movement.*

Reply:

'`OK`'

:   success

'``'

:   not supported

'`E NN`'

:   for an error
```

'`z2,addr,kind`'
'`Z2,addr,kind`'

:

```
Insert ('`Z2`.

Reply:

'`OK`'

:   success

'``'

:   not supported

'`E NN`'

:   for an error
```

'`z3,addr,kind`'
'`Z3,addr,kind`'

:

```
Insert ('`Z3`.

Reply:

'`OK`'

:   success

'``'

:   not supported

'`E NN`'

:   for an error
```

'`z4,addr,kind`'
'`Z4,addr,kind`'

:

```
Insert ('`Z4`.

Reply:

'`OK`'

:   success

'``'

:   not supported

'`E NN`'

:   for an error
```

---

::: header
Next: [Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets)]
:::
