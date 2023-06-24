---
tip: translate by openai@2023-06-23 16:55:13
...
---
description: Ada Exception GDB/MI Catchpoint Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Exception GDB/MI Catchpoint Commands (Debugging with GDB)
lang: en
resource-type: document
title: Ada Exception GDB/MI Catchpoint Commands (Debugging with GDB)
--------------------------------------------------------------------

::: header
Next: [C++ Exception GDB/MI Catchpoint Commands](C_002b_002b-Exception-GDB_002fMI-Catchpoint-Commands.html#C_002b_002b-Exception-GDB_002fMI-Catchpoint-Commands)]
:::

---

#### 27.9.2 Ada Exception [GDB/MI]

The following [GDB/MI] commands can be used to create catchpoints that stop the execution when Ada exceptions are being raised.

> 以下[GDB/MI]命令可用于创建捕获点，以便在引发 Ada 异常时停止执行。

#### The `-catch-assert` Command

#### Synopsis

::: smallexample

```bash
 -catch-assert [ -c condition] [ -d ] [ -t ]
```

:::

Add a catchpoint for failed Ada assertions.

> 添加一个用于失败的 Ada 断言的捕获点。

The possible optional parameters for this command are:

> 可选参数为：

'`-c condition`'

:   Make the catchpoint conditional on `condition`.

> 将捕获点与条件"condition"关联。

'`-d`'

:   Create a disabled catchpoint.

> 创建一个禁用的捕获点。

'`-t`'

:   Create a temporary catchpoint.

> 创建一个临时捕获点。

#### [GDB]

The corresponding [GDB]'.

> 相应的 GDB

#### Example

::: smallexample

```bash
-catch-assert
^done,bkptno="5",bkpt={number="5",type="breakpoint",disp="keep",
enabled="y",addr="0x0000000000404888",what="failed Ada assertions",
thread-groups=["i1"],times="0",
original-location="__gnat_debug_raise_assert_failure"}
(gdb)
```

:::

#### The `-catch-exception` Command

#### Synopsis

::: smallexample

```bash
 -catch-exception [ -c condition] [ -d ] [ -e exception-name ]
    [ -t ] [ -u ]
```

:::

Add a catchpoint stopping when Ada exceptions are raised. By default, the command stops the program when any Ada exception gets raised. But it is also possible, by using some of the optional parameters described below, to create more selective catchpoints.

> 添加一个捕获点，当 Ada 异常被触发时停止。默认情况下，当任何 Ada 异常被触发时，该命令会停止程序。但是，也可以通过使用下面描述的一些可选参数来创建更精确的捕获点。

The possible optional parameters for this command are:

> 可选参数有：

'`-c condition`'

:   Make the catchpoint conditional on `condition`.

> 根据条件'condition'，使捕获点成为有条件的。

'`-d`'

:   Create a disabled catchpoint.

> 创建一个禁用的捕获点。

'`-e exception-name`'

:   Only stop when `exception-name`'.

> 唯一停止的条件是 `exception-name`。

'`-t`'

:   Create a temporary catchpoint.

> 创建一个临时捕获点。

'`-u`'

:   Stop only when an unhandled exception gets raised. This option cannot be used combined with '`-e`'.

> 停止只有在未处理的异常被抛出时才停止。此选项不能与'-e'一起使用。

#### [GDB]

The corresponding [GDB]'.

> 相应的 GDB

#### Example

::: smallexample

```bash
-catch-exception -e Program_Error
^done,bkptno="4",bkpt={number="4",type="breakpoint",disp="keep",
enabled="y",addr="0x0000000000404874",
what="`Program_Error' Ada exception", thread-groups=["i1"],
times="0",original-location="__gnat_debug_raise_exception"}
(gdb)
```

:::

#### The `-catch-handlers` Command

#### Synopsis

::: smallexample

```bash
 -catch-handlers [ -c condition] [ -d ] [ -e exception-name ]
    [ -t ]
```

:::

Add a catchpoint stopping when Ada exceptions are handled. By default, the command stops the program when any Ada exception gets handled. But it is also possible, by using some of the optional parameters described below, to create more selective catchpoints.

> 添加一个捕获点，当处理 Ada 异常时停止。默认情况下，当任何 Ada 异常被处理时，该命令会停止程序。但是，也可以通过使用下面描述的一些可选参数来创建更加精确的捕获点。

The possible optional parameters for this command are:

> 可选参数为此命令有：

'`-c condition`'

:   Make the catchpoint conditional on `condition`.

> 使捕获点取决于条件 condition。

'`-d`'

:   Create a disabled catchpoint.

> 创建一个禁用的捕获点。

'`-e exception-name`'

:   Only stop when `exception-name` is handled.

> 只有在处理了 `exception-name` 异常时才停止。

'`-t`'

:   Create a temporary catchpoint.

> 创建一个临时捕获点。

#### [GDB]

The corresponding [GDB]'.

> 相应的 GDB

#### Example

::: smallexample

```bash
-catch-handlers -e Constraint_Error
^done,bkptno="4",bkpt={number="4",type="breakpoint",disp="keep",
enabled="y",addr="0x0000000000402f68",
what="`Constraint_Error' Ada exception handlers",thread-groups=["i1"],
times="0",original-location="__gnat_begin_handler"}
(gdb)
```

:::

---

::: header
Next: [C++ Exception GDB/MI Catchpoint Commands](C_002b_002b-Exception-GDB_002fMI-Catchpoint-Commands.html#C_002b_002b-Exception-GDB_002fMI-Catchpoint-Commands)]
:::
