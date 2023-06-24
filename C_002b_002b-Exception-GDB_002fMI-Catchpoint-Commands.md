---
tip: translate by openai@2023-06-23 20:11:40
...
---
description: C++ Exception GDB/MI Catchpoint Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: C++ Exception GDB/MI Catchpoint Commands (Debugging with GDB)
lang: en
resource-type: document
title: C++ Exception GDB/MI Catchpoint Commands (Debugging with GDB)
---
::: header
Previous: [Ada Exception GDB/MI Catchpoint Commands](Ada-Exception-GDB_002fMI-Catchpoint-Commands.html#Ada-Exception-GDB_002fMI-Catchpoint-Commands)]
:::

---

#### 27.9.3 C++ Exception [GDB/MI]


The following [GDB/MI] commands can be used to create catchpoints that stop the execution when C++ exceptions are being throw, rethrown, or caught.

> 以下[GDB/MI]命令可用于创建捕获点，以便在抛出、重新抛出或捕获C++异常时停止执行。

#### The `-catch-throw` Command

#### Synopsis

::: smallexample

```bash
 -catch-throw [ -t ] [ -r regexp]
```

:::


Stop when the debuggee throws a C++ exception. If `regexp` is given, then only exceptions whose type matches the regular expression will be caught.

> 停止当调试对象抛出C++异常时。如果给定`regexp`，那么只有类型与正则表达式匹配的异常才会被捕获。


If '`-t`' is given, then the catchpoint is enabled only for one stop, the catchpoint is automatically deleted after stopping once for the event.

> 如果给出't'，则只有一个停靠点会启用捕获点，捕获点在事件停止一次后会自动删除。

#### [GDB]


The corresponding [GDB]' (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)).

> 相应的GDB（参见设置捕获点）

#### Example

::: smallexample

```bash
-catch-throw -r exception_type
^done,bkpt={number="1",type="catchpoint",disp="keep",enabled="y",
  what="exception throw",catch-type="throw",
  thread-groups=["i1"],
  regexp="exception_type",times="0"}
(gdb)
-exec-run
^running
(gdb)
~"\n"
~"Catchpoint 1 (exception thrown), 0x00007ffff7ae00ed
  in __cxa_throw () from /lib64/libstdc++.so.6\n"
*stopped,bkptno="1",reason="breakpoint-hit",disp="keep",
  frame={addr="0x00007ffff7ae00ed",func="__cxa_throw",
  args=,from="/lib64/libstdc++.so.6",arch="i386:x86-64"},
  thread-id="1",stopped-threads="all",core="6"
(gdb)
```

:::

#### The `-catch-rethrow` Command

#### Synopsis

::: smallexample

```bash
 -catch-rethrow [ -t ] [ -r regexp]
```

:::


Stop when a C++ exception is re-thrown. If `regexp` is given, then only exceptions whose type matches the regular expression will be caught.

> 停止，当C++异常被重新抛出时。如果给定`regexp`，那么只有类型匹配正则表达式的异常才会被捕获。


If '`-t`' is given, then the catchpoint is enabled only for one stop, the catchpoint is automatically deleted after the first event is caught.

> 如果给出't'，那么捕获点仅针对一个站点启用，第一次捕获事件后，捕获点会自动删除。

#### [GDB]


The corresponding [GDB]' (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)).

> 相应的GDB（参见设置捕获点）

#### Example

::: smallexample

```bash
-catch-rethrow -r exception_type
^done,bkpt={number="1",type="catchpoint",disp="keep",enabled="y",
  what="exception rethrow",catch-type="rethrow",
  thread-groups=["i1"],
  regexp="exception_type",times="0"}
(gdb)
-exec-run
^running
(gdb)
~"\n"
~"Catchpoint 1 (exception rethrown), 0x00007ffff7ae00ed
  in __cxa_rethrow () from /lib64/libstdc++.so.6\n"
*stopped,bkptno="1",reason="breakpoint-hit",disp="keep",
  frame={addr="0x00007ffff7ae00ed",func="__cxa_rethrow",
  args=,from="/lib64/libstdc++.so.6",arch="i386:x86-64"},
  thread-id="1",stopped-threads="all",core="6"
(gdb)
```

:::

#### The `-catch-catch` Command

#### Synopsis

::: smallexample

```bash
 -catch-catch [ -t ] [ -r regexp]
```

:::


Stop when the debuggee catches a C++ exception. If `regexp` is given, then only exceptions whose type matches the regular expression will be caught.

> 停止当调试对象捕获C++异常时。如果给定了`regexp`，那么只有类型与正则表达式匹配的异常才会被捕获。


If '`-t`' is given, then the catchpoint is enabled only for one stop, the catchpoint is automatically deleted after the first event is caught.

> 如果给了'-t'，则只有一个停止点才启用捕获点，捕获第一个事件后捕获点会自动删除。

#### [GDB]


The corresponding [GDB]' (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)).

> 相应的GDB（参见设置捕获点）

#### Example

::: smallexample

```bash
-catch-catch -r exception_type
^done,bkpt={number="1",type="catchpoint",disp="keep",enabled="y",
  what="exception catch",catch-type="catch",
  thread-groups=["i1"],
  regexp="exception_type",times="0"}
(gdb)
-exec-run
^running
(gdb)
~"\n"
~"Catchpoint 1 (exception caught), 0x00007ffff7ae00ed
  in __cxa_begin_catch () from /lib64/libstdc++.so.6\n"
*stopped,bkptno="1",reason="breakpoint-hit",disp="keep",
  frame={addr="0x00007ffff7ae00ed",func="__cxa_begin_catch",
  args=,from="/lib64/libstdc++.so.6",arch="i386:x86-64"},
  thread-id="1",stopped-threads="all",core="6"
(gdb)
```

:::

---

::: header
Previous: [Ada Exception GDB/MI Catchpoint Commands](Ada-Exception-GDB_002fMI-Catchpoint-Commands.html#Ada-Exception-GDB_002fMI-Catchpoint-Commands)]
:::
