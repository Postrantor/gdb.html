---
description: GDB/MI File Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI File Commands (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI File Commands (Debugging with GDB)
---
::: header
Next: [GDB/MI Target Manipulation](GDB_002fMI-Target-Manipulation.html#GDB_002fMI-Target-Manipulation)]
:::

---

### 27.19 [GDB/MI]

This section describes the GDB/MI commands to specify executable file names and to read in and obtain symbol table information.

#### The `-file-exec-and-symbols` Command

#### Synopsis

::: smallexample

```bash
 -file-exec-and-symbols file
```

:::

Specify the executable file to be debugged. This file is the one from which the symbol table is also read. If no file is specified, the command clears the executable and symbol information. If breakpoints are set when using this command with no arguments, [GDB] will produce error messages. Otherwise, no output is produced, except a completion notification.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-file-exec-and-symbols /kwikemart/marge/ezannoni/TRUNK/mbx/hello.mbx
^done
(gdb)
```

:::

#### The `-file-exec-file` Command

#### Synopsis

::: smallexample

```bash
 -file-exec-file file
```

:::

Specify the executable file to be debugged. Unlike '`-file-exec-and-symbols` clears the information about the executable file. No output is produced, except a completion notification.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-file-exec-file /kwikemart/marge/ezannoni/TRUNK/mbx/hello.mbx
^done
(gdb)
```

:::

#### The `-file-list-exec-source-file` Command

#### Synopsis

::: smallexample

```bash
 -file-list-exec-source-file
```

:::

List the line number, the current source file, and the absolute path to the current source file for the current executable. The macro information field has a value of '`1`' depending on whether or not the file includes preprocessor macro information.

#### [GDB]

The [GDB]'

#### Example

::: smallexample

```bash
(gdb)
123-file-list-exec-source-file
123^done,line="1",file="foo.c",fullname="/home/bar/foo.c,macro-info="1"
(gdb)
```

:::

#### The `-file-list-exec-source-files` Command

#### Synopsis

::: smallexample

```bash
 -file-list-exec-source-files [ --group-by-objfile ]
                              [ --dirname | --basename ]
                              [ -- ]
                              [ regexp ]
```

:::

This command returns information about the source files [GDB].

With no arguments this command returns a list of source files. Each source file is represented by a tuple with the fields; `file` could become aware of additional source files.

The optional `regexp`').

If `--dirname` is provided, then `regexp` is required.

If `--group-by-objfile` is used then the format of the results is changed. The results will now be a list of tuples, with each tuple representing an object file (executable or shared library) loaded into [GDB] is a string with one of the following values:

`none`

:   This object file has no debug information.

`partially-read`

:   This object file has debug information, but it is not fully read in yet. When it is read in later, GDB might become aware of additional source files.

`fully-read`

:   This object file has debug information, and this information is fully read into GDB. The list of source files is complete.

The `sources` list can be empty for object files that have no debug information.

#### [GDB]

The [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-file-list-exec-source-files
^done,files=[,
             ,
             ]
(gdb)
-file-list-exec-source-files
^done,files=[{file="test.c",
              fullname="/tmp/info-sources/test.c",
              debug-fully-read="true"},
             {file="/usr/include/stdc-predef.h",
              fullname="/usr/include/stdc-predef.h",
              debug-fully-read="true"},
             {file="header.h",
              fullname="/tmp/info-sources/header.h",
              debug-fully-read="true"},
             {file="helper.c",
              fullname="/tmp/info-sources/helper.c",
              debug-fully-read="true"}]
(gdb)
-file-list-exec-source-files -- \\.c
^done,files=[{file="test.c",
              fullname="/tmp/info-sources/test.c",
              debug-fully-read="true"},
             {file="helper.c",
              fullname="/tmp/info-sources/helper.c",
              debug-fully-read="true"}]
(gdb)
-file-list-exec-source-files --group-by-objfile
^done,files=[{filename="/tmp/info-sources/test.x",
              debug-info="fully-read",
              sources=[{file="test.c",
                        fullname="/tmp/info-sources/test.c",
                        debug-fully-read="true"},
                       {file="/usr/include/stdc-predef.h",
                        fullname="/usr/include/stdc-predef.h",
                        debug-fully-read="true"},
                       {file="header.h",
                        fullname="/tmp/info-sources/header.h",
                        debug-fully-read="true"}]},
             {filename="/lib64/ld-linux-x86-64.so.2",
              debug-info="none",
              sources=},
             {filename="system-supplied DSO at 0x7ffff7fcf000",
              debug-info="none",
              sources=},
             {filename="/tmp/info-sources/libhelper.so",
              debug-info="fully-read",
              sources=[{file="helper.c",
                        fullname="/tmp/info-sources/helper.c",
                        debug-fully-read="true"},
                       {file="/usr/include/stdc-predef.h",
                        fullname="/usr/include/stdc-predef.h",
                        debug-fully-read="true"},
                       {file="header.h",
                        fullname="/tmp/info-sources/header.h",
                        debug-fully-read="true"}]},
             {filename="/lib64/libc.so.6",
              debug-info="none",
              sources=}]
```

:::

#### The `-file-list-shared-libraries` Command

#### Synopsis

::: smallexample

```bash
 -file-list-shared-libraries [ regexp ]
```

:::

List the shared libraries in the program. With a regular expression `regexp` are listed.

#### [GDB]

The corresponding [GDB]'. The fields have a similar meaning to the `=library-loaded` notification. The `ranges` field specifies the multiple segments belonging to this library. Each range has the following fields:

'`from`'

:   The address defining the inclusive lower bound of the segment.

'`to`'

:   The address defining the exclusive upper bound of the segment.

#### Example

::: smallexample

```bash
(gdb)
-file-list-exec-source-files
^done,shared-libraries=[
,
]
(gdb)
```

:::

#### The `-file-symbol-file` Command

#### Synopsis

::: smallexample

```bash
 -file-symbol-file file
```

:::

Read symbol table info from the specified `file`'s symbol table info. No output is produced, except for a completion notification.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-file-symbol-file /kwikemart/marge/ezannoni/TRUNK/mbx/hello.mbx
^done
(gdb)
```

:::

---

::: header
Next: [GDB/MI Target Manipulation](GDB_002fMI-Target-Manipulation.html#GDB_002fMI-Target-Manipulation)]
:::
