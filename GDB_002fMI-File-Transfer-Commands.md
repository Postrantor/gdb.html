---
description: GDB/MI File Transfer Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI File Transfer Commands (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI File Transfer Commands (Debugging with GDB)
---
::: header
Next: [GDB/MI Ada Exceptions Commands](GDB_002fMI-Ada-Exceptions-Commands.html#GDB_002fMI-Ada-Exceptions-Commands)]
:::

---

### 27.21 [GDB/MI]

#### The `-target-file-put` Command

#### Synopsis

::: smallexample

```bash
 -target-file-put hostfile targetfile
```

:::

Copy file `hostfile` on the target system.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-target-file-put localfile remotefile
^done
(gdb)
```

:::

#### The `-target-file-get` Command

#### Synopsis

::: smallexample

```bash
 -target-file-get targetfile hostfile
```

:::

Copy file `targetfile` on the host system.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-target-file-get remotefile localfile
^done
(gdb)
```

:::

#### The `-target-file-delete` Command

#### Synopsis

::: smallexample

```bash
 -target-file-delete targetfile
```

:::

Delete `targetfile` from the target system.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-target-file-delete remotefile
^done
(gdb)
```

:::
