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

#### The `-catch-throw` Command

#### Synopsis

::: smallexample

```bash
 -catch-throw [ -t ] [ -r regexp]
```

:::

Stop when the debuggee throws a C++ exception. If `regexp` is given, then only exceptions whose type matches the regular expression will be caught.

If '`-t`' is given, then the catchpoint is enabled only for one stop, the catchpoint is automatically deleted after stopping once for the event.

#### [GDB]

The corresponding [GDB]' (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)).

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

If '`-t`' is given, then the catchpoint is enabled only for one stop, the catchpoint is automatically deleted after the first event is caught.

#### [GDB]

The corresponding [GDB]' (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)).

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

If '`-t`' is given, then the catchpoint is enabled only for one stop, the catchpoint is automatically deleted after the first event is caught.

#### [GDB]

The corresponding [GDB]' (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)).

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
