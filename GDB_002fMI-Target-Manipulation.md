---
tip: translate by openai@2023-06-23 22:17:38
...
---
description: GDB/MI Target Manipulation (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Target Manipulation (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Target Manipulation (Debugging with GDB)
---
::: header
Next: [GDB/MI File Transfer Commands](GDB_002fMI-File-Transfer-Commands.html#GDB_002fMI-File-Transfer-Commands)]
:::

---

### 27.20 [GDB/MI]

#### The `-target-attach` Command

#### Synopsis

::: smallexample

```bash
 -target-attach pid | gid | file
```

:::

Attach to a process `pid`' must be used.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-target-attach 34
=thread-created,id="1"
*stopped,thread-id="1",frame=
^done
(gdb)
```

:::

#### The `-target-detach` Command

#### Synopsis

::: smallexample

```bash
 -target-detach [ pid | gid ]
```

:::


Detach from the remote target which normally resumes its execution. If either `pid` is specified, detaches from either the specified process, or specified thread group. There's no output.

> 从远程目标断开连接，通常会恢复其执行。如果指定了`pid`，则从指定的进程或指定的线程组中断开连接。没有输出。

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-target-detach
^done
(gdb)
```

:::

#### The `-target-disconnect` Command

#### Synopsis

::: smallexample

```bash
 -target-disconnect
```

:::


Disconnect from the remote target. There's no output and the target is generally not resumed.

> 断开远程目标。没有输出，目标通常不会恢复。

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-target-disconnect
^done
(gdb)
```

:::

#### The `-target-download` Command

#### Synopsis

::: smallexample

```bash
 -target-download
```

:::


Loads the executable onto the remote target. It prints out an update message every half second, which includes the fields:

> 将可执行文件加载到远程目标上。每隔半秒会打印一条更新消息，包括以下字段：

'`section`'

:   The name of the section.

'`section-sent`'

:   The size of what has been sent so far for that section.

'`section-size`'

:   The size of the section.

'`total-sent`'


:   The total size of what was sent so far (the current and the previous sections).

> 总共发送的大小（当前和之前的部分）。

'`total-size`'

:   The size of the overall executable to download.


Each message is sent as status record (see [[GDB/MI] Output Syntax](GDB_002fMI-Output-Syntax.html#GDB_002fMI-Output-Syntax)).

> 每条消息都以状态记录的形式发送（请参阅[[GDB/MI] Output Syntax](GDB_002fMI-Output-Syntax.html#GDB_002fMI-Output-Syntax))。


In addition, it prints the name and size of the sections, as they are downloaded. These messages include the following fields:

> 此外，它还会打印下载时的部分名称和大小。这些消息包括以下字段：

'`section`'

:   The name of the section.

'`section-size`'

:   The size of the section.

'`total-size`'

:   The size of the overall executable to download.

At the end, a summary is printed.

#### [GDB]

The corresponding [GDB]'.

#### Example


Note: each status message appears on a single line. Here the messages have been broken down so that they can fit onto a page.

> 注意：每条状态消息在单独的一行中显示。为了适应页面，这里的消息已经分行显示。

::: smallexample

```bash
(gdb)
-target-download
+download,
+download,{section=".text",section-sent="512",section-size="6668",
total-sent="512",total-size="9880"}
+download,{section=".text",section-sent="1024",section-size="6668",
total-sent="1024",total-size="9880"}
+download,{section=".text",section-sent="1536",section-size="6668",
total-sent="1536",total-size="9880"}
+download,{section=".text",section-sent="2048",section-size="6668",
total-sent="2048",total-size="9880"}
+download,{section=".text",section-sent="2560",section-size="6668",
total-sent="2560",total-size="9880"}
+download,{section=".text",section-sent="3072",section-size="6668",
total-sent="3072",total-size="9880"}
+download,{section=".text",section-sent="3584",section-size="6668",
total-sent="3584",total-size="9880"}
+download,{section=".text",section-sent="4096",section-size="6668",
total-sent="4096",total-size="9880"}
+download,{section=".text",section-sent="4608",section-size="6668",
total-sent="4608",total-size="9880"}
+download,{section=".text",section-sent="5120",section-size="6668",
total-sent="5120",total-size="9880"}
+download,{section=".text",section-sent="5632",section-size="6668",
total-sent="5632",total-size="9880"}
+download,{section=".text",section-sent="6144",section-size="6668",
total-sent="6144",total-size="9880"}
+download,{section=".text",section-sent="6656",section-size="6668",
total-sent="6656",total-size="9880"}
+download,
+download,
+download,
+download,{section=".data",section-sent="512",section-size="3156",
total-sent="7236",total-size="9880"}
+download,{section=".data",section-sent="1024",section-size="3156",
total-sent="7748",total-size="9880"}
+download,{section=".data",section-sent="1536",section-size="3156",
total-sent="8260",total-size="9880"}
+download,{section=".data",section-sent="2048",section-size="3156",
total-sent="8772",total-size="9880"}
+download,{section=".data",section-sent="2560",section-size="3156",
total-sent="9284",total-size="9880"}
+download,{section=".data",section-sent="3072",section-size="3156",
total-sent="9796",total-size="9880"}
^done,address="0x10004",load-size="9880",transfer-rate="6586",
write-rate="429"
(gdb)
```

:::

#### [GDB]

No equivalent.

#### Example

N.A.

#### The `-target-flash-erase` Command

#### Synopsis

::: smallexample

```bash
 -target-flash-erase
```

:::

Erases all known flash memory regions on the target.

The corresponding [GDB]'.


The output is a list of flash regions that have been erased, with starting addresses and memory region sizes.

> 输出是一个已擦除的闪存区域列表，包括起始地址和内存区域大小。

::: smallexample

```bash
(gdb)
-target-flash-erase
^done,erased-regions=
(gdb)
```

:::

#### The `-target-select` Command

#### Synopsis

::: smallexample

```bash
 -target-select type parameters …
```

:::

Connect [GDB] to the remote target. This command takes two args:

'`type`'

:   The type of target, for instance '`remote`', etc.

'`parameters`'


:   Device names, host names and the like. See [Commands for Managing Targets](Target-Commands.html#Target-Commands), for more details.

> 设备名称、主机名等。有关更多详情，请参见[管理目标的命令](Target-Commands.html#Target-Commands)。


The output is a connection notification, followed by the address at which the target program is, in the following form:

> 输出是一个连接通知，其次是目标程序所在的地址，格式如下：

::: smallexample

```bash
^connected,addr="address",func="function name",
  args=[arg list]
```

:::

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-target-select remote /dev/ttya
^connected,addr="0xfe00a300",func="??",args=
(gdb)
```

:::

---

::: header
Next: [GDB/MI File Transfer Commands](GDB_002fMI-File-Transfer-Commands.html#GDB_002fMI-File-Transfer-Commands)]
:::
