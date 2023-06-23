---
tip: translate by openai@2023-06-23 14:46:03
...
---
description: Tracepoint Packets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Tracepoint Packets (Debugging with GDB)
lang: en
resource-type: document
title: Tracepoint Packets (Debugging with GDB)
----------------------------------------------

::: header
Next: [Host I/O Packets](Host-I_002fO-Packets.html#Host-I_002fO-Packets)]
:::

---

### E.6 Tracepoint Packets

Here we describe the packets [GDB] uses to implement tracepoints (see [Tracepoints](Tracepoints.html#Tracepoints)).

> 在这里，我们描述 GDB 使用的数据包来实现跟踪点（参见[跟踪点](Tracepoints.html#Tracepoints)）。

'`QTDP:n:addr:ena:step:pass[:Fflen][:Xlen,bytes][-]`'

> QTDP：n：addr：ena：步骤：pass[：Fflen][：Xlen，字节][-]

:

```
Create a new tracepoint, number `n`' packets will follow to specify this tracepoint's actions.

Replies:

'`OK`'

:   The packet was understood and carried out.

'`qRelocInsn`'

:   See [Relocate instruction reply packet](#Tracepoint-Packets).

'``'

:   The packet was not recognized.
```

'`QTDP:-n:addr:[S]action…[-]`'

> QTDP：-n：addr：[S]行动...[-]

:   Define actions to be taken when a tracepoint is hit. The `n`' packets will follow, specifying more actions for this tracepoint.

> 当跟踪点被命中时，定义所采取的行动。 `n` 个数据包将随后指定此跟踪点的更多行动。

```
In the series of action packets for a given tracepoint, at most one can have an '`S`', then all the packets in the series specify ordinary tracepoint actions.

The '`action…`' portion of the packet is a series of actions, concatenated without separators. Each action has one of the following forms:

'`R mask`'

:   Collect the registers whose bits are set in `mask` may be any number of digits long; it may not fit in a 32-bit word.

'`M basereg,offset,len`'

:   Collect `len` is a special case).

'`X len,expr`'

:   Evaluate `expr` is the number of bytes in the expression (and thus one-half the number of hex digits in the packet).

Any number of actions may be packed together in a single '`QTDP`' action. (The "while-stepping" actions are treated as if they were attached to a separate tracepoint, as far as these restrictions are concerned.)

Replies:

'`OK`'

:   The packet was understood and carried out.

'`qRelocInsn`'

:   See [Relocate instruction reply packet](#Tracepoint-Packets).

'``'

:   The packet was not recognized.
```

'`QTDPsrc:n:addr:type:start:slen:bytes`'

> QTDPsrc：n：addr：type：start：slen：bytes

:

```
Specify a source string of tracepoint `n` is the string, encoded in hexadecimal.

`start` is the total length of the source string. This is intended for handling source strings that are longer than will fit in a single packet.

The available string types are '`at` sends a separate packet for each command in the action list, in the same order in which the commands are stored in the list.

The target does not need to do anything with source strings except report them back as part of the replies to the '`qTfP`' query packets.

Although this packet is optional, and [GDB]' not to work, or a particular trace frame not be found.
```

'`QTDV:n:value:builtin:name`'

> 'QTDV：n：值：内置：名称'

:

```
Create a new trace state variable, number `n`') of the trace state variable.
```

'`QTFrame:n`'

:

```
Select the `n`.

A successful reply from the stub indicates that the stub has found the requested frame. The response is a series of parts, concatenated without separators, describing the frame we selected. Each part has one of the following forms:

'`F f`'

:   The selected frame is number `n`', then there was no frame matching the criteria in the request packet.

'`T t`'

:   The selected trace frame records a hit of tracepoint number `t` is a hexadecimal number.
```

'`QTFrame:pc:addr`'

:   Like '`QTFrame:n` is a hexadecimal number.

> QTFrame:n 是一个十六进制数字。

'`QTFrame:tdp:t`'

:   Like '`QTFrame:n` is a hexadecimal number.

> QTFrame:n 是一个十六进制数字。

'`QTFrame:range:start:end`'

> QTFrame：范围：开始：结束

:   Like '`QTFrame:n` are hexadecimal numbers.

> 像'QTFrame:n'这样的十六进制数字。

'`QTFrame:outside:start:end`'

> QTFrame：外部：开始：结束

:   Like '`QTFrame:range:start:end`', but select the first frame *outside* the given range of addresses (exclusive).

> 像'`QTFrame:range:start:end`'，但选择给定地址范围之外的第一帧（排除）。

'`qTMinFTPILen`'

:

```
This packet requests the minimum length of instruction at which a fast tracepoint (see [Set Tracepoints](Set-Tracepoints.html#Set-Tracepoints)) may be placed. For instance, on the 32-bit x86 architecture, it is possible to use a 4-byte jump, but it depends on the target system being able to create trampolines in the first 64K of memory, which might or might not be possible for that system. So the reply to this packet will be 4 if it is able to arrange for that.

Replies:

'`0`'

:   The minimum instruction length is currently unknown.

'`length`'

:   The minimum instruction length is `length` is a hexadecimal number greater or equal to 1. A reply of 1 means that a fast tracepoint may be placed on any instruction regardless of size.

'`E`'

:   An error has occurred.

'``'

:   An empty reply indicates that the request is not supported by the stub.
```

'`QTStart`'

:

```
Begin the tracepoint experiment. Begin collecting data from tracepoint hits in the trace frame buffer. This packet supports the '`qRelocInsn`' reply (see [Relocate instruction reply packet](#Tracepoint-Packets)).
```

'`QTStop`'

:

```
End the tracepoint experiment. Stop collecting trace frames.
```

'`QTEnable:n:addr`'

:

```
Enable tracepoint `n` in a started tracepoint experiment. If the tracepoint was previously disabled, then collection of data from it will resume.
```

'`QTDisable:n:addr`'

:

```
Disable tracepoint `n`' is subsequently issued.
```

'`QTinit`'

:

```
Clear the table of tracepoints, and empty the trace frame buffer.
```

'`QTro:start1,end1:start2,end2:…`'

> QTro：开始 1，结束 1：开始 2，结束 2：…

:

```
Establish the given ranges of memory as "transparent". The stub will answer requests for these ranges from memory's current contents, if they were not collected as part of the tracepoint hit.

[GDB] uses this to mark read-only regions of memory, like those containing program code. Since these areas never change, they should still have the same contents they did when the tracepoint was hit, so there's no reason for the stub to refuse to provide their contents.
```

'`QTDisconnected:value`'

> QT 已断开连接：值

:

```
Set the choice to what to do with the tracing run when [GDB] is no longer in the picture.
```

'`qTStatus`'

:

```
Ask the stub if there is a trace experiment running right now.

The reply has the form:

'`Trunning[;field]…`'

:   `running` is a single digit `1` if the trace is presently running, or `0` if not. It is followed by semicolon-separated optional fields that an agent may use to report additional status.

If the trace is not running, the agent may report any of several explanations as one of the optional fields:

'`tnotrun:0`'

:   No trace has been run yet.

'`tstop[:text]:0`'

:   The trace was stopped by a user-originated stop command. The optional `text` field is a user-supplied string supplied as part of the stop command (for instance, an explanation of why the trace was stopped manually). It is hex-encoded.

'`tfull:0`'

:   The trace stopped because the trace buffer filled up.

'`tdisconnected:0`'

:   The trace stopped because [GDB] disconnected from the target.

'`tpasscount:tpnum`'

:   The trace stopped because tracepoint `tpnum` exceeded its pass count.

'`terror:text:tpnum`'

:   The trace stopped because tracepoint `tpnum` is available to describe the nature of the error (for instance, a divide by zero in the condition expression); it is hex encoded.

'`tunknown:0`'

:   The trace stopped for some other reason.

Additional optional fields supply statistical and other information. Although not required, they are extremely useful for users monitoring the progress of a trace run. If a trace has stopped, and these numbers are reported, they must reflect the state of the just-stopped trace.

'`tframes:n`'

:   The number of trace frames in the buffer.

'`tcreated:n`'

:   The total number of trace frames created during the run. This may be larger than the trace frame count, if the buffer is circular.

'`tsize:n`'

:   The total size of the trace buffer, in bytes.

'`tfree:n`'

:   The number of bytes still unused in the buffer.

'`circular:n`'

:   The value of the circular trace buffer flag. `1` means that the trace buffer is circular and old trace frames will be discarded if necessary to make room, `0` means that the trace buffer is linear and may fill up.

'`disconn:n`'

:   The value of the disconnected tracing flag. `1` means that tracing will continue after [GDB] disconnects, `0` means that the trace run will stop.
```

'`qTP:tp:addr`'

:

```
Ask the stub for the current state of tracepoint number `tp`.

Replies:

'`Vhits:usage`'

:   The tracepoint has been hit `hits` in the trace buffer. Note that `while-stepping` steps are not counted as separate hits, but the steps' space consumption is added into the usage number.
```

'`qTV:var`'

:

```
Ask the stub for the value of the trace state variable number `var`.

Replies:

'`Vvalue`'

:   The value of the variable is `value`. This will be the current value of the variable if the user is examining a running target, or a saved value if the variable was collected in the trace frame that the user is looking at. Note that multiple requests may result in different reply values, such as when requesting values while the program is running.

'`U`'

:   The value of the variable is unknown. This would occur, for example, if the user is examining a trace frame in which the requested variable was not collected.
```

| '`qTfP`' |
| :------: |

'`qTsP`'

:

```
These packets request data about tracepoints that are being used by the target. [GDB] sends `qTfP` to get the first piece of data, and multiple `qTsP` to get additional pieces. Replies to these packets generally take the form of the `QTDP` packets that define tracepoints. (FIXME add detailed syntax)
```

| '`qTfV`' |
| :------: |

'`qTsV`'

:

```
These packets request data about trace state variables that are on the target. [GDB] sends `qTfV` to get the first vari of data, and multiple `qTsV` to get additional variables. Replies to these packets follow the syntax of the `QTDV` packets that define trace state variables.
```

'`qTfSTM`'
'`qTsSTM`'

:

```
These packets request data about static tracepoint markers that exist in the target program. [GDB] sends `qTfSTM` to get the first piece of data, and multiple `qTsSTM` to get additional pieces. Replies to these packets take the following form:

Reply:

'`m address:id:extra`'

:   A single marker

'`m address:id:extra,address:id:extra…`'

:   a comma-separated list of markers

'`l`'

:   (lower case letter '`L`') denotes end of list.

'`E nn`'

:   An error occurred. The error number `nn` is given as hex digits.

'``'

:   An empty reply indicates that the request is not supported by the stub.

The `address` are strings encoded in hex.

In response to each query, the target will reply with a list of one or more markers, separated by commas. [GDB]' (lower-case ell, for *last*).
```

'`qTSTMat:address`'

:

```
This packets requests data about static tracepoint markers in the target program at `address`' and `qTsSTM` packets that list static tracepoint markers.
```

'`QTSave:filename`'

:

```
This packet directs the target to save trace data to the file name `filename` is encoded as a hex string; the interpretation of the file name (relative vs absolute, wild cards, etc) is up to the target.
```

'`qTBuffer:offset,len`'

:

```
Return up to `len`. The trace buffer is treated as if it were a contiguous collection of traceframes, as per the trace file format. The reply consists as many hex-encoded bytes as the target can deliver in a packet; it is not an error to return fewer than were asked for. A reply consisting of just `l` indicates that no bytes are available.
```

'`QTBuffer:circular:value`'

> 'QTBuffer：环形：值'

:   This packet directs the target to use a circular trace buffer if `value` is 1, or a linear buffer if the value is 0.

> 如果 `值` 为 1，此数据包指示目标使用圆形跟踪缓冲区，如果值为 0，则使用线性缓冲区。

'`QTBuffer:size:size`'

:

```
This packet directs the target to make the trace buffer be of size `size` if possible. A value of `-1` tells the target to use whatever size it prefers.
```

'`QTNotes:[type:text][;type:text]…`'

> 'QTNotes:[类型：文本][;类型：文本]…'

:

```
This packet adds optional textual notes to the trace run. Allowable types include `user`, `notes`, and `tstop`, the `text` fields are arbitrary strings, hex-encoded.
```

#### E.6.1 Relocate instruction reply packet

When installing fast tracepoints in memory, the target may need to relocate the instruction currently at the tracepoint address to a different address in memory. For most instructions, a simple copy is enough, but, for example, call instructions that implicitly push the return address on the stack, and relative branches or other PC-relative instructions require offset adjustment, so that the effect of executing the instruction at a different address is the same as if it had executed in the original location.

> 当在内存中安装快速跟踪点时，目标可能需要将当前位于跟踪点地址的指令重新定位到内存中的不同地址。对于大多数指令，只需要简单复制即可，但是，例如隐式将返回地址压入堆栈的调用指令以及相对分支或其他基于 PC 的相对指令，需要调整偏移量，以便在不同地址处执行指令的效果与在原始位置执行指令的效果相同。

In response to several of the tracepoint packets, the target may also respond with a number of intermediate '`qRelocInsn`' packets. The format of the request is:

> 对于几个跟踪点数据包，目标也可能以许多中间的'qRelocInsn'数据包做出响应。请求的格式是：

'`qRelocInsn:from;to`'

:   This requests [GDB].

> 这个请求[GDB]。

Replies:

'`qRelocInsn:adjusted_size`'

> qRelocInsn：调整后的大小

:   Informs the stub the relocation is complete. The `adjusted_size` is the length in bytes of resulting relocated instruction sequence.

> 通知存根重定位已完成。`adjusted_size` 是重定位指令序列的字节长度。

'`E NN`'

:   A badly formed request was detected, or an error was encountered while relocating the instruction.

> 检测到错误格式的请求，或者在重定位指令时遇到错误。

---

::: header
Next: [Host I/O Packets](Host-I_002fO-Packets.html#Host-I_002fO-Packets)]
:::
