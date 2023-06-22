---
description: libthread_db.so.1 file (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: libthread_db.so.1 file (Debugging with GDB)
lang: en
resource-type: document
title: libthread_db.so.1 file (Debugging with GDB)
---
::: header
Next: [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)]
:::

---

#### 22.8.2 Automatically loading thread debugging library

This feature is currently present only on [GNU]/Linux native hosts.

[GDB] reads in some cases thread debugging library from places specific to the inferior (see [set libthread-db-search-path](Threads.html#set-libthread_002ddb_002dsearch_002dpath)).

The special '`libthread-db-search-path`' is enabled before trying to open such thread debugging library.

Note that loading of this debugging library also requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

`set auto-load libthread-db [on|off]`

Enable or disable the auto-loading of inferior specific thread debugging library.

`show auto-load libthread-db`

Show whether auto-loading of inferior specific thread debugging library is enabled or disabled.

`info auto-load libthread-db`

Print the list of all loaded inferior specific thread debugging libraries and for each such library print list of inferior `pid` s using it.
