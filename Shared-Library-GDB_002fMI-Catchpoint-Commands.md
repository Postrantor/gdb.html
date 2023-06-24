---
tip: translate by openai@2023-06-24 02:53:57
...
---
description: Shared Library GDB/MI Catchpoint Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Shared Library GDB/MI Catchpoint Commands (Debugging with GDB)
lang: en
resource-type: document
title: Shared Library GDB/MI Catchpoint Commands (Debugging with GDB)
---
::: header
Next: [Ada Exception GDB/MI Catchpoint Commands](Ada-Exception-GDB_002fMI-Catchpoint-Commands.html#Ada-Exception-GDB_002fMI-Catchpoint-Commands)]
:::

---

#### 27.9.1 Shared Library [GDB/MI]

#### The `-catch-load` Command

#### Synopsis

::: smallexample

```bash
 -catch-load [ -t ] [ -d ] regexp
```

:::


Add a catchpoint for library load events. If the '`-t`' argument is a regular expression used to match the name of the loaded library.

> 添加一个库加载事件的捕获点。如果'`-t`'参数是一个用于匹配已加载库名称的正则表达式。

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
-catch-load -t foo.so
^done,bkpt={number="1",type="catchpoint",disp="del",enabled="y",
what="load of library matching foo.so",catch-type="load",times="0"}
(gdb)
```

:::

#### The `-catch-unload` Command

#### Synopsis

::: smallexample

```bash
 -catch-unload [ -t ] [ -d ] regexp
```

:::


Add a catchpoint for library unload events. If the '`-t`' argument is a regular expression used to match the name of the unloaded library.

> 添加一个用于库卸载事件的捕获点。如果'-t'参数是一个用于匹配卸载库的名称的正则表达式。

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
-catch-unload -d bar.so
^done,bkpt={number="2",type="catchpoint",disp="keep",enabled="n",
what="load of library matching bar.so",catch-type="unload",times="0"}
(gdb)
```

:::
