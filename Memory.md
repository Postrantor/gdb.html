---
description: Memory (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Memory (Debugging with GDB)
lang: en
resource-type: document
title: Memory (Debugging with GDB)
---
::: header
Next: [Memory Tagging](Memory-Tagging.html#Memory-Tagging)]
:::

---

### 10.6 Examining Memory

You can use the command `x` (for "examine") to examine memory in any of several formats, independently of your program's data types.

`x/nfu addr`

`x addr`

`x`

Use the `x` command to examine memory.

`n`.

[`n`

:   The repeat count is a decimal integer; the default is 1. It specifies how much memory (counting by units `u`.

[`f`

:   The display format is one of the formats used by `print` ('`x`' (hexadecimal) initially. The default changes each time you use either `x` or `print`.

[`u`

:   The unit size is any of

```
`b`

:   Bytes.

`h`

:   Halfwords (two bytes).

`w`

:   Words (four bytes). This is the initial default.

`g`

:   Giant words (eight bytes).

Each time you specify a unit size with `x`, that size becomes the default unit the next time you use `x`. For the '`i`' will use UTF-32. The encoding is set by the programming language and cannot be altered.
```

[`addr`

:   `addr` is usually just after the last address examined---but several other commands also set the default address: `info breakpoints` (to the address of the last breakpoint listed), `info line` (to the starting address of a line), and `print` (if you use it to display a value from memory).

For example, '`x/3uh 0x54320`').

You can also specify a negative repeat count to examine memory backward from the given address. For example, '`x/-3uh 0x54320`' prints three halfwords (`h`) at `0x5431a`, `0x5431c`, and `0x5431e`.

Since the letters indicating unit sizes are all distinct from the letters specifying output formats, you do not have to remember whether unit size or format comes first; either order works. The output specifications '`4xw`' does not work.)

Even though the unit size `u`' format also prints branch delay slot instructions, if any, beyond the count specified, which immediately follow the last instruction that is within the count. The command `disassemble` gives an alternative way of inspecting machine instructions; see [Source and Machine Code](Machine-Code.html#Machine-Code).

If a negative repeat count is specified for the formats '`s`' format, we use line number information in the debug info to accurately locate instruction boundaries while disassembling backward. If line info is not available, the command stops examining memory with an error message.

All the defaults for the arguments to `x` are designed to make it easy to continue scanning memory with minimal specifications each time you use `x`. For example, after you have inspected three machine instructions with '`x/3i addr` is used again; the other arguments default as for successive uses of `x`.

When examining machine instructions, the instruction at current program counter is shown with a `=>` marker. For example:

::: smallexample

```bash
(gdb) x/5i $pc-6
   0x804837f <main+11>: mov    %esp,%ebp
   0x8048381 <main+13>: push   %ecx
   0x8048382 <main+14>: sub    $0x4,%esp
=> 0x8048385 <main+17>: movl   $0x8048460,(%esp)
   0x804838c <main+24>: call   0x80482d4 <puts@plt>
```

:::

If the architecture supports memory tagging, the tags can be displayed by using '`m`'. See [Memory Tagging](Memory-Tagging.html#Memory-Tagging).

The information will be displayed once per granule size (the amount of bytes a particular memory tag covers). For example, AArch64 has a granule size of 16 bytes, so it will display a tag every 16 bytes.

Due to the way [GDB] prints information with the `x` command (not aligned to a particular boundary), the tag information will refer to the initial address displayed on a particular line. If a memory tag boundary is crossed in the middle of a line displayed by the `x` command, it will be displayed on the next line.

The '`m`' format doesn't affect any other specified formats that were passed to the `x` command.

The addresses and contents printed by the `x` command are not saved in the value history because there is often too much of them and they would get in the way. Instead, [GDB] makes these values available for subsequent use in expressions as values of the convenience variables `$_` and `$__`. After an `x` command, the last address examined is available for use in expressions in the convenience variable `$_`. The contents of that address, as examined, are available in the convenience variable `$__`.

If the `x` command has a repeat count, the address and contents saved are from the last memory unit printed; this is not the same as the last address printed if several units were printed on the last line of output.

Most targets have an addressable memory unit size of 8 bits. This means that to each memory address are associated 8 bits of data. Some targets, however, have other addressable memory unit sizes. Within [GDB] and this document, the term *addressable memory unit* (or *memory unit* for short) is used when explicitly referring to a chunk of data of that size. The word *byte* is used to refer to a chunk of data of 8 bits, regardless of the addressable memory unit size of the target. For most systems, addressable memory unit is a synonym of byte.

When you are debugging a program running on a remote target machine (see [Remote Debugging](Remote-Debugging.html#Remote-Debugging)), you may wish to verify the program's image in the remote machine's memory against the executable file you downloaded to the target. Or, on any target, you may want to check whether the program has corrupted its own read-only sections. The `compare-sections` command is provided for such situations.

`compare-sections [section-name|-r`]

Compare the data of a loadable section `section-name` in the executable file of the program being debugged with the same section in the target machine's memory, and report any mismatches. With no arguments, compares all loadable sections. With an argument of `-r`, compares all loadable read-only sections.

Note: for remote targets, this command can be accelerated if the target supports computing the CRC checksum of a block of memory (see [qCRC packet](General-Query-Packets.html#qCRC-packet)).

---

::: header
Next: [Memory Tagging](Memory-Tagging.html#Memory-Tagging)]
:::
