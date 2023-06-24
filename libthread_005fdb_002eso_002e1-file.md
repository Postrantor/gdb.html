---
tip: translate by openai@2023-06-23 23:50:44
...
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

> GDB 在某些情况下会从特定于被调试进程的位置读取线程调试库（参见[设置 libthread-db-search-path](Threads.html#set-libthread_002ddb_002dsearch_002dpath)）。


The special '`libthread-db-search-path`' is enabled before trying to open such thread debugging library.

> 特殊的“libthread-db-search-path”在尝试打开这样的线程调试库之前已启用。


Note that loading of this debugging library also requires accordingly configured `auto-load safe-path` (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)).

> 注意，加载此调试库也需要相应配置的“自动加载安全路径”（参见[自动加载安全路径](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)）。

`set auto-load libthread-db [on|off]`


Enable or disable the auto-loading of inferior specific thread debugging library.

> 启用或禁用自动加载特定于次级的线程调试库。

`show auto-load libthread-db`


Show whether auto-loading of inferior specific thread debugging library is enabled or disabled.

> 检查自动加载特定线程调试库是否已启用或已禁用。

`info auto-load libthread-db`


Print the list of all loaded inferior specific thread debugging libraries and for each such library print list of inferior `pid` s using it.

> 打印所有已加载的特定于次级的线程调试库的列表，并为每个库打印使用它的次级`pid`列表。
