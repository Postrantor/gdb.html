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

The intent of this section is to provide extra minimal debugging information for use in simple backtraces. It is not intended to be a replacement for full separate debugging information (see [Separate Debug Files](Separate-Debug-Files.html#Separate-Debug-Files)). The example below shows the intended use; however, [GDB] does not currently put restrictions on what sort of debugging information might be included in the section.

[GDB] was configured with LZMA support.

This section can be easily created using `objcopy` and other standard utilities:

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
