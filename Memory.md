---
tip: translate by openai@2023-06-24 00:17:34
...
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

> 你可以使用命令`x`（代表“检查”）来以多种格式独立于你的程序数据类型检查内存。

`x/nfu addr`

`x addr`

`x`

Use the `x` command to examine memory.

`n`.

[`n`


:   The repeat count is a decimal integer; the default is 1. It specifies how much memory (counting by units `u`.

> 重复计数是一个十进制整数；默认值为1。它指定以单位u计算的内存大小。

[`f`


:   The display format is one of the formats used by `print` ('`x`' (hexadecimal) initially. The default changes each time you use either `x` or `print`.

> 显示格式是`print`使用的格式之一（最初是'x'（十六进制））。每次使用`x`或`print`时，默认格式会发生变化。

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

> `addr`通常只是在最后一个检查过的地址之后-但是其他几个命令也可以设置默认地址：`info breakpoints`（到最后一个断点列出的地址），`info line`（到一行的起始地址）和`print`（如果你用它来从内存中显示一个值）。

For example, '`x/3uh 0x54320`').


You can also specify a negative repeat count to examine memory backward from the given address. For example, '`x/-3uh 0x54320`' prints three halfwords (`h`) at `0x5431a`, `0x5431c`, and `0x5431e`.

> 你也可以指定一个负数的重复计数，从给定的地址向后检查内存。例如，`x/-3uh 0x54320`会打印出位于`0x5431a`，`0x5431c`和`0x5431e`的三个半字（`h`）。


Since the letters indicating unit sizes are all distinct from the letters specifying output formats, you do not have to remember whether unit size or format comes first; either order works. The output specifications '`4xw`' does not work.)

> 由于用于表示单位大小的字母与用于指定输出格式的字母是不同的，因此您不必记住单位大小或格式哪个先出现；两者都可以。输出规格“4xw”无效。


Even though the unit size `u`' format also prints branch delay slot instructions, if any, beyond the count specified, which immediately follow the last instruction that is within the count. The command `disassemble` gives an alternative way of inspecting machine instructions; see [Source and Machine Code](Machine-Code.html#Machine-Code).

> 即使单元大小`u`格式也会打印出支持延迟槽指令（如果有的话），这些指令会立即跟随计数范围内的最后一条指令。命令`disassemble`提供了一种检查机器指令的替代方式；请参见[源代码和机器码](Machine-Code.html#Machine-Code)。


If a negative repeat count is specified for the formats '`s`' format, we use line number information in the debug info to accurately locate instruction boundaries while disassembling backward. If line info is not available, the command stops examining memory with an error message.

> 如果为“s”格式指定了负重复计数，我们将使用调试信息中的行号信息准确定位指令边界，以便反汇编。如果没有行信息，命令将停止使用错误消息检查内存。


All the defaults for the arguments to `x` are designed to make it easy to continue scanning memory with minimal specifications each time you use `x`. For example, after you have inspected three machine instructions with '`x/3i addr` is used again; the other arguments default as for successive uses of `x`.

> 所有`x`的参数的默认值都旨在使每次使用`x`时，可以以最少的规格继续扫描内存。例如，在使用“x/3i addr”检查了三条机器指令后，其他参数会按照`x`的连续使用默认。


When examining machine instructions, the instruction at current program counter is shown with a `=>` marker. For example:

> 在检查机器指令时，当前程序计数器上的指令用`=>`标记显示。例如：

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

> 如果架构支持内存标记，可以使用“m”来显示标记。详见[内存标记](Memory-Tagging.html#Memory-Tagging)。


The information will be displayed once per granule size (the amount of bytes a particular memory tag covers). For example, AArch64 has a granule size of 16 bytes, so it will display a tag every 16 bytes.

> 信息将每个粒度大小（特定内存标签所覆盖的字节数）显示一次。例如，AArch64具有16字节的粒度大小，因此它将每16字节显示一个标签。


Due to the way [GDB] prints information with the `x` command (not aligned to a particular boundary), the tag information will refer to the initial address displayed on a particular line. If a memory tag boundary is crossed in the middle of a line displayed by the `x` command, it will be displayed on the next line.

> 由于GDB使用`x`命令打印信息（不对齐特定边界），标签信息将指向特定行上显示的初始地址。如果`x`命令显示的行中跨越了内存标签边界，它将显示在下一行。


The '`m`' format doesn't affect any other specified formats that were passed to the `x` command.

> 'm'格式不会影响传递给'x'命令的其他指定格式。


The addresses and contents printed by the `x` command are not saved in the value history because there is often too much of them and they would get in the way. Instead, [GDB] makes these values available for subsequent use in expressions as values of the convenience variables `$_` and `$__`. After an `x` command, the last address examined is available for use in expressions in the convenience variable `$_`. The contents of that address, as examined, are available in the convenience variable `$__`.

> `x` 命令打印的地址和内容不会保存到值历史中，因为它们通常数量太多，会挡住路。相反，[GDB]将这些值提供给后续在表达式中使用，作为便利变量 `$_` 和 `$__` 的值。在执行 `x` 命令后，最后一个检查的地址可用于表达式中的便利变量 `$_`。检查的地址内容可在便利变量 `$__` 中获取。


If the `x` command has a repeat count, the address and contents saved are from the last memory unit printed; this is not the same as the last address printed if several units were printed on the last line of output.

> 如果`x`命令有重复计数，则所保存的地址和内容都是来自最后一个内存单元；如果最后一行输出中打印了几个单元，这将不同于最后打印的地址。


Most targets have an addressable memory unit size of 8 bits. This means that to each memory address are associated 8 bits of data. Some targets, however, have other addressable memory unit sizes. Within [GDB] and this document, the term *addressable memory unit* (or *memory unit* for short) is used when explicitly referring to a chunk of data of that size. The word *byte* is used to refer to a chunk of data of 8 bits, regardless of the addressable memory unit size of the target. For most systems, addressable memory unit is a synonym of byte.

> 大多数目标具有8位可寻址内存单元的大小。这意味着每个内存地址都关联着8位的数据。但是，有些目标具有其他可寻址内存单元的大小。在[GDB]和本文档中，当明确指的是该大小的数据块时，使用术语“可寻址内存单元”（或简称为“内存单元”）。单词“字节”用于指8位的数据块，而不管目标的可寻址内存单元的大小。对于大多数系统，可寻址内存单元是字节的同义词。


When you are debugging a program running on a remote target machine (see [Remote Debugging](Remote-Debugging.html#Remote-Debugging)), you may wish to verify the program's image in the remote machine's memory against the executable file you downloaded to the target. Or, on any target, you may want to check whether the program has corrupted its own read-only sections. The `compare-sections` command is provided for such situations.

> 当您在远程目标机器上调试程序时（参见[远程调试](Remote-Debugging.html#Remote-Debugging)），您可能希望验证远程机器内存中的程序映像与您下载到目标的可执行文件是否相同。或者，在任何目标上，您可能希望检查程序是否损坏了自己的只读部分。为此，提供了`compare-sections`命令。

`compare-sections [section-name|-r`]


Compare the data of a loadable section `section-name` in the executable file of the program being debugged with the same section in the target machine's memory, and report any mismatches. With no arguments, compares all loadable sections. With an argument of `-r`, compares all loadable read-only sections.

> 比较调试程序的可加载段`section-name`在可执行文件中的数据与目标机器内存中的相同段的数据，并报告任何不匹配。如果没有参数，则比较所有可加载段。如果参数为`-r`，则比较所有可加载只读段。


Note: for remote targets, this command can be accelerated if the target supports computing the CRC checksum of a block of memory (see [qCRC packet](General-Query-Packets.html#qCRC-packet)).

> 注意：对于远程目标，如果目标支持计算内存块的CRC校验和（参见[qCRC数据包](General-Query-Packets.html#qCRC-packet)），则可以加速此命令。

---

::: header
Next: [Memory Tagging](Memory-Tagging.html#Memory-Tagging)]
:::
