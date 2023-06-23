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

Benefits of the `-gdb.ext` way:

- Can be used with file formats that don't support multiple sections.
- Ease of finding scripts for public libraries.

  Scripts specified in the `.debug_gdb_scripts` section are searched for in the source search path. For publicly installed libraries, e.g., `libstdc++`, there typically isn't a source directory in which to find the script.
- Doesn't require source code additions.

Benefits of the `.debug_gdb_scripts` way:

- Works with static linking.

  Scripts for libraries done the `-gdb.ext` script.
- Works with classes that are entirely inlined.

  Some classes can be entirely inlined, and thus there may not be an associated shared library to attach a `-gdb.ext` script to.
- Scripts needn't be copied out of the source tree.

  In some circumstances, apps can be built out of large collections of internal libraries, and the build infrastructure necessary to install the `-gdb.ext` can find them is cumbersome. It may be easier to specify the scripts in the `.debug_gdb_scripts` section as relative paths, and add a path to the top of the source tree to the source search path.
