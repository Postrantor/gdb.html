---
tip: translate by openai@2023-06-23 17:46:44
...
---
description: Auto-loading verbose mode (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Auto-loading verbose mode (Debugging with GDB)
lang: en
resource-type: document
title: Auto-loading verbose mode (Debugging with GDB)
---
::: header
Previous: [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)]
:::

---

#### 22.8.4 Displaying files tried for auto-load


For better visibility of all the file locations where you can place scripts to be auto-loaded with inferior --- or to protect yourself against accidental execution of untrusted scripts --- [GDB] provides a feature for printing all the files attempted to be loaded. Both existing and non-existing files may be printed.

> 为了更好地查看所有可以放置脚本以便自动加载到次级 - 或者为了保护自己免受误执行不受信任脚本的影响 - [GDB] 提供了一个打印所有尝试加载的文件的功能。无论是现有的还是不存在的文件都可以打印出来。


For example the list of directories from which it is safe to auto-load files (see [Auto-loading safe path](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)) applies also to canonicalized filenames which may not be too obvious while setting it up.

> 举例来说，安全自动加载文件的目录列表（参见[自动加载安全路径](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)）也适用于规范化的文件名，在设置时可能不太明显。

::: smallexample

```bash
(gdb) set debug auto-load on
(gdb) file ~/src/t/true
auto-load: Loading canned sequences of commands script "/tmp/true-gdb.gdb"
           for objfile "/tmp/true".
auto-load: Updating directories of "/usr:/opt".
auto-load: Using directory "/usr".
auto-load: Using directory "/opt".
warning: File "/tmp/true-gdb.gdb" auto-loading has been declined
         by your `auto-load safe-path' set to "/usr:/opt".
```

:::

`set debug auto-load [on|off]`


Set whether to print the filenames attempted to be auto-loaded.

> 设置是否打印尝试自动加载的文件名。

`show debug auto-load`


Show whether printing of the filenames attempted to be auto-loaded is turned on or off.

> 显示尝试自动加载的文件名是否已打开或关闭。
