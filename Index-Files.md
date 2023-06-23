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

::: smallexample

```bash
$ gdb-add-index symfile
```

:::

See [gdb-add-index](gdb_002dadd_002dindex-man.html#gdb_002dadd_002dindex).

It is also possible to do the work manually. Here is what `gdb-add-index` does behind the curtains.

The index is stored as a section in the symbol file. [GDB] can write the index to a file, then you can put it into the symbol file using `objcopy`.

To create an index file, use the `save gdb-index` command:

`save gdb-index [-dwarf-5] directory`

:

```
Create index files for all symbol files currently known by [GDB].
```

Once you have created an index file you can merge it into your symbol file, here named `symfile`, using `objcopy`:

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

*Warning:* Setting `use-deprecated-index-sections` to `on` must be done before gdb reads the file. The following will not work:

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

`set index-cache enabled on`

`set index-cache enabled off`

Enable or disable the use of the symbol index cache.

`set index-cache directory directory`

`show index-cache directory`

Set/show the directory where index files will be saved.

The default value for this directory depends on the host platform. On most systems, the index is cached in the `gdb` subdirectory of your home directory. However, on some systems, the default may differ according to local convention.

There is no limit on the disk space used by index cache. It is perfectly safe to delete the content of that directory to free up disk space.

`show index-cache stats`

Print the number of cache hits and misses since the launch of [GDB].

---

::: header
Next: [Symbol Errors](Symbol-Errors.html#Symbol-Errors)]
:::
