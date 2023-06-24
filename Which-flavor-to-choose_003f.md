---
tip: translate by openai@2023-06-24 04:45:45
...
---
description: Which flavor to choose? (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Which flavor to choose? (Debugging with GDB)
lang: en
resource-type: document
title: Which flavor to choose? (Debugging with GDB)
---
::: header
Previous: [dotdebug_gdb_scripts section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)]
:::

---

#### 23.5.3 Which flavor to choose?


Given the multiple ways of auto-loading extensions, it might not always be clear which one to choose. This section provides some guidance.

> 给出多种自动加载扩展的方式，可能并不总是清楚该选择哪一个。本节提供一些指导。

Benefits of the `-gdb.ext` way:

- Can be used with file formats that don't support multiple sections.
- Ease of finding scripts for public libraries.


  Scripts specified in the `.debug_gdb_scripts` section are searched for in the source search path. For publicly installed libraries, e.g., `libstdc++`, there typically isn't a source directory in which to find the script.

> `.debug_gdb_scripts` 部分指定的脚本会在源搜索路径中搜索。对于公开安装的库，例如`libstdc++`，通常没有源目录可以找到脚本。
- Doesn't require source code additions.

Benefits of the `.debug_gdb_scripts` way:

- Works with static linking.

  Scripts for libraries done the `-gdb.ext` script.
- Works with classes that are entirely inlined.


  Some classes can be entirely inlined, and thus there may not be an associated shared library to attach a `-gdb.ext` script to.

> 一些类可以完全内联，因此可能没有相关的共享库来附加`-gdb.ext`脚本。
- Scripts needn't be copied out of the source tree.


  In some circumstances, apps can be built out of large collections of internal libraries, and the build infrastructure necessary to install the `-gdb.ext` can find them is cumbersome. It may be easier to specify the scripts in the `.debug_gdb_scripts` section as relative paths, and add a path to the top of the source tree to the source search path.

> 在某些情况下，可以使用大量内部库构建应用程序，而安装`-gdb.ext`所需的构建基础结构可能很麻烦。可能更容易在`.debug_gdb_scripts`部分指定相对路径，并将源树的顶部路径添加到源搜索路径中。
