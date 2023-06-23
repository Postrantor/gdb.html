---
description: Ada Exception GDB/MI Catchpoint Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Ada Exception GDB/MI Catchpoint Commands (Debugging with GDB)
lang: en
resource-type: document
title: Ada Exception GDB/MI Catchpoint Commands (Debugging with GDB)
---
::: header
Next: [C++ Exception GDB/MI Catchpoint Commands](C_002b_002b-Exception-GDB_002fMI-Catchpoint-Commands.html#C_002b_002b-Exception-GDB_002fMI-Catchpoint-Commands)]
:::

---

#### 27.9.2 Ada Exception [GDB/MI]

The following [GDB/MI] commands can be used to create catchpoints that stop the execution when Ada exceptions are being raised.

#### The `-catch-assert` Command

#### Synopsis

::: smallexample

```bash
 -catch-assert [ -c condition] [ -d ] [ -t ]
```

:::

Add a catchpoint for failed Ada assertions.

The possible optional parameters for this command are:

'`-c condition`'

:   Make the catchpoint conditional on `condition`.

'`-d`'

:   Create a disabled catchpoint.

'`-t`'

:   Create a temporary catchpoint.

#### [GDB]

The corresponding [GDB]'.

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

The possible optional parameters for this command are:

'`-c condition`'

:   Make the catchpoint conditional on `condition`.

'`-d`'

:   Create a disabled catchpoint.

'`-e exception-name`'

:   Only stop when `exception-name`'.

'`-t`'

:   Create a temporary catchpoint.

'`-u`'

:   Stop only when an unhandled exception gets raised. This option cannot be used combined with '`-e`'.

#### [GDB]

The corresponding [GDB]'.

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

The possible optional parameters for this command are:

'`-c condition`'

:   Make the catchpoint conditional on `condition`.

'`-d`'

:   Create a disabled catchpoint.

'`-e exception-name`'

:   Only stop when `exception-name` is handled.

'`-t`'

:   Create a temporary catchpoint.

#### [GDB]

The corresponding [GDB]'.

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
