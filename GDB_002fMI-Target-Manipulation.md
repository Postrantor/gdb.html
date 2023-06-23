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

'`section`'

:   The name of the section.

'`section-sent`'

:   The size of what has been sent so far for that section.

'`section-size`'

:   The size of the section.

'`total-sent`'

:   The total size of what was sent so far (the current and the previous sections).

'`total-size`'

:   The size of the overall executable to download.

Each message is sent as status record (see [[GDB/MI] Output Syntax](GDB_002fMI-Output-Syntax.html#GDB_002fMI-Output-Syntax)).

In addition, it prints the name and size of the sections, as they are downloaded. These messages include the following fields:

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

The output is a connection notification, followed by the address at which the target program is, in the following form:

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
