---
description: GDB/MI Program Context (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Program Context (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Program Context (Debugging with GDB)
---
::: header
Next: [GDB/MI Thread Commands](GDB_002fMI-Thread-Commands.html#GDB_002fMI-Thread-Commands)]
:::

---

### 27.10 [GDB/MI]

#### The `-exec-arguments` Command

#### Synopsis

::: smallexample

```bash
 -exec-arguments args
```

:::

Set the inferior program arguments, to be used in the next '`-exec-run`'.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-exec-arguments -v word
^done
(gdb)
```

:::

#### The `-environment-cd` Command

#### Synopsis

::: smallexample

```bash
 -environment-cd pathdir
```

:::

Set [GDB]'s working directory.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-environment-cd /kwikemart/marge/ezannoni/flathead-dev/devo/gdb
^done
(gdb)
```

:::

#### The `-environment-directory` Command

#### Synopsis

::: smallexample

```bash
 -environment-directory [ -r ] [ pathdir ]+
```

:::

Add directories `pathdir`' option, the search path is first reset and then addition occurs as normal. Multiple directories may be specified, separated by blanks. Specifying multiple directories in a single command results in the directories added to the beginning of the search path in the same order they were presented in the command. If blanks are needed as part of a directory name, double-quotes should be used around the name. In the command output, the path will show up separated by the system directory-separator character. The directory-separator character must not be used in any directory name. If no directories are specified, the current search path is displayed.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-environment-directory /kwikemart/marge/ezannoni/flathead-dev/devo/gdb
^done,source-path="/kwikemart/marge/ezannoni/flathead-dev/devo/gdb:$cdir:$cwd"
(gdb)
-environment-directory ""
^done,source-path="/kwikemart/marge/ezannoni/flathead-dev/devo/gdb:$cdir:$cwd"
(gdb)
-environment-directory -r /home/jjohnstn/src/gdb /usr/src
^done,source-path="/home/jjohnstn/src/gdb:/usr/src:$cdir:$cwd"
(gdb)
-environment-directory -r
^done,source-path="$cdir:$cwd"
(gdb)
```

:::

#### The `-environment-path` Command

#### Synopsis

::: smallexample

```bash
 -environment-path [ -r ] [ pathdir ]+
```

:::

Add directories `pathdir`' option, the search path is first reset and then addition occurs as normal. Multiple directories may be specified, separated by blanks. Specifying multiple directories in a single command results in the directories added to the beginning of the search path in the same order they were presented in the command. If blanks are needed as part of a directory name, double-quotes should be used around the name. In the command output, the path will show up separated by the system directory-separator character. The directory-separator character must not be used in any directory name. If no directories are specified, the current path is displayed.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-environment-path
^done,path="/usr/bin"
(gdb)
-environment-path /kwikemart/marge/ezannoni/flathead-dev/ppc-eabi/gdb /bin
^done,path="/kwikemart/marge/ezannoni/flathead-dev/ppc-eabi/gdb:/bin:/usr/bin"
(gdb)
-environment-path -r /usr/local/bin
^done,path="/usr/local/bin:/usr/bin"
(gdb)
```

:::

#### The `-environment-pwd` Command

#### Synopsis

::: smallexample

```bash
 -environment-pwd
```

:::

Show the current working directory.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-environment-pwd
^done,cwd="/kwikemart/marge/ezannoni/flathead-dev/devo/gdb"
(gdb)
```

:::

---

::: header
Next: [GDB/MI Thread Commands](GDB_002fMI-Thread-Commands.html#GDB_002fMI-Thread-Commands)]
:::
