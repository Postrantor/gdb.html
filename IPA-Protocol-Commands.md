---
tip: translate by openai@2023-06-23 23:39:35
...
---
description: IPA Protocol Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: IPA Protocol Commands (Debugging with GDB)
lang: en
resource-type: document
title: IPA Protocol Commands (Debugging with GDB)
---
::: header
Previous: [IPA Protocol Objects](IPA-Protocol-Objects.html#IPA-Protocol-Objects)]
:::

---

#### 31.1.2 IPA Protocol Commands


The spaces in each command are delimiters to ease reading this commands specification. They don't exist in real commands.

> 命令中的空格是为了便于阅读命令规范而设置的分隔符，实际命令中不存在。

'`FastTrace:tracepoint_object gdb_jump_pad_head`'


:   Installs a new fast tracepoint described by `tracepoint_object`, 8-byte long, is the head of *jumppad*, which is used to jump to data collection routine in IPA finally.

> 安装一个新的快速跟踪点，由`tracepoint_object`描述，长8字节，是*jumppad*的头，最终被用来跳转到IPA中的数据收集例程。

```
Replies:

'`OK target_address gdb_jump_pad_head fjump_size fjump`'

:   `target_address`.

'`E NN`'

:   for an error
```

'`close`'


:   Closes the in-process agent. This command is sent when [GDB] or GDBserver is about to kill inferiors.

> 关闭正在进行的代理。当[GDB]或GDBserver准备杀死下级时，会发出此命令。

'`qTfSTM`'

:   See [qTfSTM](Tracepoint-Packets.html#qTfSTM).

'`qTsSTM`'

:   See [qTsSTM](Tracepoint-Packets.html#qTsSTM).

'`qTSTMat`'

:   See [qTSTMat](Tracepoint-Packets.html#qTSTMat).

'`probe_marker_at:address`'

:   Asks in-process agent to probe the marker at `address`.

```
Replies:

'`E NN`'

:   for an error
```

'`unprobe_marker_at:address`'

:   Asks in-process agent to unprobe the marker at `address`.
