---
tip: translate by openai@2023-06-24 00:22:09
...
---
description: MiniDebugInfo (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: MiniDebugInfo (Debugging with GDB)
lang: en
resource-type: document
title: MiniDebugInfo (Debugging with GDB)
---
::: header
Next: [Index Files](Index-Files.html#Index-Files)]
:::

---

### 18.4 Debugging information in a special section


Some systems ship pre-built executables and libraries that have a special '`.gnu_debugdata`' section. This feature is called *MiniDebugInfo*. This section holds an LZMA-compressed object and is used to supply extra symbols for backtraces.

> 一些系统会发布预先构建的可执行文件和库，这些库具有特殊的“.gnu_debugdata”部分。这一特性被称为*MiniDebugInfo*。该部分包含一个LZMA压缩的对象，用于提供回溯的额外符号。


The intent of this section is to provide extra minimal debugging information for use in simple backtraces. It is not intended to be a replacement for full separate debugging information (see [Separate Debug Files](Separate-Debug-Files.html#Separate-Debug-Files)). The example below shows the intended use; however, [GDB] does not currently put restrictions on what sort of debugging information might be included in the section.

> 本节的意图是为简单的回溯提供额外的最小调试信息。它不是用于完整的单独调试信息的替代品（参见[单独调试文件]（Separate-Debug-Files.html#Separate-Debug-Files））。下面的示例显示了预期的用法；但是，[GDB]不会对可能包含在该节中的任何类型的调试信息施加限制。

[GDB] was configured with LZMA support.


This section can be easily created using `objcopy` and other standard utilities:

> 这部分可以使用`objcopy`和其他标准工具轻松创建：

::: smallexample

```bash
# Extract the dynamic symbols from the main binary, there is no need
# to also have these in the normal symbol table.
nm -D binary --format=posix --defined-only \
  | awk '' | sort > dynsyms

# Extract all the text (i.e. function) symbols from the debuginfo.
# (Note that we actually also accept "D" symbols, for the benefit
# of platforms like PowerPC64 that use function descriptors.)
nm binary --format=posix --defined-only \
  | awk '' \
  | sort > funcsyms

# Keep all the function symbols not already in the dynamic symbol
# table.
comm -13 dynsyms funcsyms > keep_symbols

# Separate full debug info into debug binary.
objcopy --only-keep-debug binary debug

# Copy the full debuginfo, keeping only a minimal set of symbols and
# removing some unnecessary sections.
objcopy -S --remove-section .gdb_index --remove-section .comment \
  --keep-symbols=keep_symbols debug mini_debuginfo

# Drop the full debug info from the original binary.
strip --strip-all -R .comment binary

# Inject the compressed data into the .gnu_debugdata section of the
# original binary.
xz mini_debuginfo
objcopy --add-section .gnu_debugdata=mini_debuginfo.xz binary
```

:::

---

::: header
Next: [Index Files](Index-Files.html#Index-Files)]
:::
