---
tip: translate by openai@2023-06-24 00:41:27
...
---
description: objfile-gdbdotext file (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: objfile-gdbdotext file (Debugging with GDB)
lang: en
resource-type: document
title: objfile-gdbdotext file (Debugging with GDB)
---
::: header
Next: [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)]
:::

---

#### 23.5.1 The `objfile-gdb.ext`


When a new object file is read, [GDB] is the file extension for the extension language:

> 当读取一个新的对象文件时，[GDB]是扩展语言的文件扩展名。

`objfile-gdb.gdb`

:   GDB's own command language

`objfile-gdb.py`

:   Python

`objfile-gdb.scm`

:   Guile

`script-name` will evaluate it as a script in the specified extension language.


If this file does not exist, then [GDB], because Windows filesystems disallow colons in file names.)

> 如果这个文件不存在，那么[GDB]，因为Windows文件系统不允许在文件名中使用冒号。


Note that loading of these files requires an accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

> 注意，加载这些文件需要相应配置的“自动加载安全路径”（参见[自动加载安全路径](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)）。


For object files using `.exe` stripping is case insensitive and it is attempted on any platform. This makes the script filenames compatible between Unix and MS-Windows hosts.

> 对于使用`.exe`后缀的对象文件，剥离是不区分大小写的，并且可以在任何平台上尝试。这使得脚本文件名在Unix和MS-Windows主机之间兼容。

`set auto-load scripts-directory [directories]`

Control [GDB]' on MS-Windows and MS-DOS).


Each entry here needs to be covered also by the security setting `set auto-load safe-path` (see [set auto-load safe-path](Auto_002dloading-safe-path.html#set-auto_002dload-safe_002dpath)).

> 每个条目都需要由安全设置`set auto-load safe-path`覆盖（参见[设置自动加载安全路径](Auto_002dloading-safe-path.html#set-auto_002dload-safe_002dpath))。

This variable defaults to `$debugdir:$datadir/auto-load`.


Any reference to `$debugdir` directory separators, depending on the host platform.

> 任何涉及`$debugdir`目录分隔符的引用，取决于主机平台。


The list of directories uses path separator ('`:`' on MS-Windows and MS-DOS) to separate directories, similarly to the `PATH` environment variable.

> 目录列表使用路径分隔符（在MS-Windows和MS-DOS中为“：”）来分隔目录，类似于`PATH`环境变量。

`show auto-load scripts-directory`

Show [GDB] auto-loaded scripts location.

`add-auto-load-scripts-directory [directories…]`


Add an entry (or list of entries) to the list of auto-loaded scripts locations. Multiple entries may be delimited by the host platform path separator in use.

> 向自动加载脚本位置列表中添加一个（或多个）条目。多个条目可以用所使用的主机平台路径分隔符进行分隔。


[GDB] file should be careful to avoid errors if it is evaluated more than once.

> 应该小心处理[GDB]文件，以避免如果被多次评估时出现错误。

---

::: header
Next: [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)]
:::
