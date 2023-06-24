---
tip: translate by openai@2023-06-23 23:15:24
...
---
description: Index Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Index Files (Debugging with GDB)
lang: en
resource-type: document
title: Index Files (Debugging with GDB)
---
::: header
Next: [Symbol Errors](Symbol-Errors.html#Symbol-Errors)]
:::

---

### 18.5 Index Files Speed Up [GDB]

When [GDB] provides a way to build an index, which speeds up startup.


For convenience, [GDB] comes with a program, `gdb-add-index`, which can be used to add the index to a symbol file. It takes the symbol file as its only argument:

> 为了方便起见，[GDB]附带了一个程序`gdb-add-index`，用于向符号文件添加索引。它将符号文件作为唯一的参数：

::: smallexample

```bash
$ gdb-add-index symfile
```

:::


See [gdb-add-index](gdb_002dadd_002dindex-man.html#gdb_002dadd_002dindex).

> 看[gdb-add-index](gdb_002dadd_002dindex-man.html#gdb_002dadd_002dindex)。


It is also possible to do the work manually. Here is what `gdb-add-index` does behind the curtains.

> 也可以手动完成这项工作。这是`gdb-add-index`背后所做的事情。


The index is stored as a section in the symbol file. [GDB] can write the index to a file, then you can put it into the symbol file using `objcopy`.

> 索引被存储在符号文件的一个部分中。[GDB] 可以将索引写入文件，然后可以使用`objcopy`将其放入符号文件中。

To create an index file, use the `save gdb-index` command:

`save gdb-index [-dwarf-5] directory`

:

```
Create index files for all symbol files currently known by [GDB].
```


Once you have created an index file you can merge it into your symbol file, here named `symfile`, using `objcopy`:

> 一旦创建了索引文件，您就可以使用`objcopy`将其合并到您的符号文件（这里称为`symfile`）中：

::: smallexample

```bash
$ objcopy --add-section .gdb_index=symfile.gdb-index \
    --set-section-flags .gdb_index=readonly symfile symfile
```

:::

Or for `-dwarf-5`:

::: smallexample

```bash
$ objcopy --dump-section .debug_str=symfile.debug_str.new symfile
$ cat symfile.debug_str >>symfile.debug_str.new
$ objcopy --add-section .debug_names=symfile.gdb-index \
    --set-section-flags .debug_names=readonly \
    --update-section .debug_str=symfile.debug_str.new symfile symfile
```

:::


[GDB] to use a deprecated index section anyway specify `set use-deprecated-index-sections on`. The default is `off`. This can speed up startup, but may result in some functionality being lost. See [Index Section Format](Index-Section-Format.html#Index-Section-Format).

> 在GDB中，要使用不推荐使用的索引部分，请指定`set use-deprecated-index-sections on`。默认情况下是`off`。这可以加快启动速度，但可能会导致某些功能丢失。请参阅[索引部分格式](Index-Section-Format.html#Index-Section-Format)。


*Warning:* Setting `use-deprecated-index-sections` to `on` must be done before gdb reads the file. The following will not work:

> *警告：*必须在GDB读取文件之前将“use-deprecated-index-sections”设置为“on”。以下操作无效：

::: smallexample

```bash
$ gdb -ex "set use-deprecated-index-sections on" <program>
```

:::

Instead you must do, for example,

::: smallexample

```bash
$ gdb -iex "set use-deprecated-index-sections on" <program>
```

:::

Indices only work when using DWARF debugging information, not stabs.

#### 18.5.1 Automatic symbol index cache


It is possible for [GDB]. The following commands can be used to tweak the behavior of the index cache.

> 可以对[GDB]进行调整。可以使用以下命令来调整索引缓存的行为。

`set index-cache enabled on`

`set index-cache enabled off`

Enable or disable the use of the symbol index cache.

`set index-cache directory directory`

`show index-cache directory`

Set/show the directory where index files will be saved.


The default value for this directory depends on the host platform. On most systems, the index is cached in the `gdb` subdirectory of your home directory. However, on some systems, the default may differ according to local convention.

> 默认值取决于主机平台。在大多数系统上，索引会被缓存在您家目录的`gdb`子目录中。但是，在某些系统上，根据本地惯例，默认值可能有所不同。


There is no limit on the disk space used by index cache. It is perfectly safe to delete the content of that directory to free up disk space.

> 没有限制索引缓存所使用的磁盘空间。删除该目录的内容以释放磁盘空间是完全安全的。

`show index-cache stats`

Print the number of cache hits and misses since the launch of [GDB].

---

::: header
Next: [Symbol Errors](Symbol-Errors.html#Symbol-Errors)]
:::
