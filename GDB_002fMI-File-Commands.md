---
tip: translate by openai@2023-06-23 21:57:47
...
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

> 这一节描述了GDB/MI命令，用于指定可执行文件名称，并读入和获取符号表信息。

#### The `-file-exec-and-symbols` Command

#### Synopsis

::: smallexample

```bash
 -file-exec-and-symbols file
```

:::


Specify the executable file to be debugged. This file is the one from which the symbol table is also read. If no file is specified, the command clears the executable and symbol information. If breakpoints are set when using this command with no arguments, [GDB] will produce error messages. Otherwise, no output is produced, except a completion notification.

> 指定要调试的可执行文件。这个文件也是读取符号表的文件。如果没有指定文件，该命令将清除可执行文件和符号信息。如果在使用此命令时没有参数设置断点，[GDB]将生成错误消息。否则，除了完成通知外，不会产生任何输出。

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

> 指定要调试的可执行文件。与'-file-exec-and-symbols'不同，它会清除有关可执行文件的信息。除了完成通知外，不会产生任何输出。

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

> 列出当前可执行文件的行号、当前源文件和当前源文件的绝对路径。宏信息字段的值取决于该文件是否包含预处理器宏信息，值为“1”。

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

> 没有参数时，此命令会返回一个源文件列表。每个源文件由元组表示，字段包括：“文件”可以获知额外的源文件。

The optional `regexp`').

If `--dirname` is provided, then `regexp` is required.


If `--group-by-objfile` is used then the format of the results is changed. The results will now be a list of tuples, with each tuple representing an object file (executable or shared library) loaded into [GDB] is a string with one of the following values:

> 如果使用`--group-by-objfile`，则结果的格式将发生变化。结果现在将是一个元组列表，每个元组代表一个加载到[GDB]中的可执行文件（可执行文件或共享库），其值为以下之一：

`none`

:   This object file has no debug information.

`partially-read`


:   This object file has debug information, but it is not fully read in yet. When it is read in later, GDB might become aware of additional source files.

> 这个对象文件有调试信息，但尚未完全读取。稍后读取时，GDB可能会意识到额外的源文件。

`fully-read`


:   This object file has debug information, and this information is fully read into GDB. The list of source files is complete.

> 这个对象文件有调试信息，这些信息已被完全读入GDB中。源文件列表是完整的。


The `sources` list can be empty for object files that have no debug information.

> 分析对象文件无调试信息时，`源`列表可以是空的。

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

> 使用正则表达式`regexp`列出程序中的共享库。

#### [GDB]


The corresponding [GDB]'. The fields have a similar meaning to the `=library-loaded` notification. The `ranges` field specifies the multiple segments belonging to this library. Each range has the following fields:

> 相应的[GDB]。字段具有与`=library-loaded`通知类似的含义。`ranges`字段指定属于此库的多个段。每个范围具有以下字段：

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

> 从指定的文件的符号表信息中读取符号表信息。除了完成通知外，不产生任何输出。

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
