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

'`FastTrace:tracepoint_object gdb_jump_pad_head`'

:   Installs a new fast tracepoint described by `tracepoint_object`, 8-byte long, is the head of *jumppad*, which is used to jump to data collection routine in IPA finally.

```
Replies:

'`OK target_address gdb_jump_pad_head fjump_size fjump`'

:   `target_address`.

'`E NN`'

:   for an error
```

'`close`'

:   Closes the in-process agent. This command is sent when [GDB] or GDBserver is about to kill inferiors.

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
