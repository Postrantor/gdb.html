---
tip: translate by openai@2023-06-23 21:53:22
...
---
description: GDB/MI Data Manipulation (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Data Manipulation (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Data Manipulation (Debugging with GDB)
---
::: header
Next: [GDB/MI Tracepoint Commands](GDB_002fMI-Tracepoint-Commands.html#GDB_002fMI-Tracepoint-Commands)]
:::

---

### 27.16 [GDB/MI]


This section describes the [GDB/MI] commands that manipulate data: examine memory and registers, evaluate expressions, etc.

> 这一节描述了操作数据的[GDB/MI]命令：检查内存和寄存器、求表达式的值等。


For details about what an addressable memory unit is, see [addressable memory unit](Memory.html#addressable-memory-unit).

> 对于有关可寻址存储单元的详细信息，请参阅[可寻址存储单元](Memory.html#addressable-memory-unit)。

#### The `-data-disassemble` Command

#### Synopsis

::: smallexample

```bash
 -data-disassemble
  ( -s start-addr -e end-addr
  | -a addr
  | -f filename -l linenum [ -n lines ] )
  [ --opcodes opcodes-mode ]
  [ --source ]
  [ -- mode ]
```

:::

Where:

'`start-addr`'

:   is the beginning address (or `$pc`)

'`end-addr`'

:   is the end address

'`addr`'


:   is an address anywhere within (or the name of) the function to disassemble. If an address is specified, the whole function surrounding that address will be disassembled. If a name is specified, the whole function with that name will be disassembled.

> ': 是一个地址（或函数名），可以用来反汇编。如果指定了地址，则会反汇编整个围绕该地址的函数。如果指定了名称，则会反汇编整个具有该名称的函数。

'`filename`'

:   is the name of the file to disassemble

'`linenum`'

:   is the line number to disassemble around

'`lines`'


:   is the number of disassembly lines to be produced. If it is -1, the whole function will be disassembled, in case no `end-addr` are displayed.

> `:` 是要生成的反汇编行数。如果它是-1，则整个函数将被反汇编，如果不显示`end-addr`。

'`opcodes-mode`'

:   can only be used with `mode` 0, and should be one of the following:

```
'`none`'

:   no opcode information will be included in the result.

'`bytes`'

:   opcodes will be included in the result, the opcodes will be formatted as for [disassemble /b].

'`display`'

:   opcodes will be included in the result, the opcodes will be formatted as for [disassemble /r].
```

'`mode`'

:   the use of `mode` should be one of:

```
'`0`'

:   *disassembly only*, this is the default mode if no mode is specified.

'`1`'

:   *mixed source and disassembly (deprecated)*, it is not possible to recreate this mode using `--opcodes` and `--source` options.

'`2`'

:   *disassembly with raw opcodes*, this mode is equivalent to using `mode` 0 and passing `--opcodes bytes` to the command.

'`3`'

:   *mixed source and disassembly with raw opcodes (deprecated)*, it is not possible to recreate this mode using `--opcodes` and `--source` options.

'`4`'

:   *mixed source and disassembly*, this mode is equivalent to using `mode` 0 and passing `--source` to the command.

'`5`'

:   *mixed source and disassembly with raw opcodes*, this mode is equivalent to using `mode` 0 and passing `--opcodes bytes` and `--source` to the command.

Modes 1 and 3 are deprecated. The output is "source centric" which hasn't proved useful in practice. See [Machine Code](Machine-Code.html#Machine-Code), for a discussion of the difference between `/m` and `/s` output of the `disassemble` command.
```

The `--source` can only be used with `mode` 4 or 5 had been used.

#### Result


The result of the `-data-disassemble` command will be a list named '`asm_insns`', the contents of this list depend on the options used with the `-data-disassemble` command.

> 结果`-data-disassemble`命令将会是一个名为'`asm_insns`'的列表，该列表的内容取决于与`-data-disassemble`命令一起使用的选项。


For modes 0 and 2, and when the `--source` option is not used, the '`asm_insns`' list contains tuples with the following fields:

> 对于模式0和2，当不使用`--source`选项时，'`asm_insns`'列表包含具有以下字段的元组：

`address`

:   The address at which this instruction was disassembled.

`func-name`

:   The name of the function this instruction is within.

`offset`

:   The decimal offset in bytes from the start of '`func-name`'.

`inst`

:   The text disassembly for this '`address`'.

`opcodes`


:   This field is only present for modes 2, 3 and 5, or when the `--opcodes` option '`bytes`' field.

> 此字段只在模式2、3和5出现，或者当使用`--opcodes`选项时出现`bytes`字段时出现。

```
When the '`--opcodes`](Machine-Code.html#disassemble)).

When '`--opcodes` command.
```


For modes 1, 3, 4 and 5, or when the `--source` option is used, the '`asm_insns`', each of which has the following fields:

> 对于模式1、3、4和5，或者使用`--source`选项时，'`asm_insns`'拥有以下字段：

`line`

:   The line number within '`file`'.

`file`


:   The file name from the compilation unit. This might be an absolute file name or a relative file name depending on the compile command used.

> 文件名来自编译单元。这可能是一个绝对文件名或相对文件名，取决于使用的编译命令。

`fullname`


:   Absolute file name of '`file`'. It is converted to a canonical form using the source file search path (see [Specifying Source Directories](Source-Path.html#Source-Path)) and after resolving all the symbolic links.

> 绝对文件名'`file`'。它使用源文件搜索路径（参见[指定源目录](Source-Path.html#Source-Path)）转换为规范形式，并解析所有符号链接后。

```
If the source file is not found this field will contain the path as present in the debug information.
```

`line_asm_insn`

:   This is a list of tuples containing the disassembly for '`line`'.


Note that whatever included in the '`inst`, i.e., it is not possible to adjust its format.

> 注意，不可能调整`inst`中包含的任何内容的格式。

#### [GDB]

The corresponding [GDB]'.

#### Example

Disassemble from the current value of `$pc` to `$pc + 20`:

::: smallexample

```bash
(gdb)
-data-disassemble -s $pc -e "$pc + 20" -- 0
^done,
asm_insns=[
{address="0x000107c0",func-name="main",offset="4",
inst="mov  2, %o0"},
{address="0x000107c4",func-name="main",offset="8",
inst="sethi  %hi(0x11800), %o2"},
{address="0x000107c8",func-name="main",offset="12",
inst="or  %o2, 0x140, %o1\t! 0x11940 <_lib_version+8>"},
{address="0x000107cc",func-name="main",offset="16",
inst="sethi  %hi(0x11800), %o2"},
{address="0x000107d0",func-name="main",offset="20",
inst="or  %o2, 0x168, %o4\t! 0x11968 <_lib_version+48>"}]
(gdb)
```

:::

Disassemble the whole `main` function. Line 32 is part of `main`.

::: smallexample

```bash
-data-disassemble -f basics.c -l 32 -- 0
^done,asm_insns=[
{address="0x000107bc",func-name="main",offset="0",
inst="save  %sp, -112, %sp"},
{address="0x000107c0",func-name="main",offset="4",
inst="mov   2, %o0"},
{address="0x000107c4",func-name="main",offset="8",
inst="sethi %hi(0x11800), %o2"},
[…]
,
]
(gdb)
```

:::

Disassemble 3 instructions from the start of `main`:

::: smallexample

```bash
(gdb)
-data-disassemble -f basics.c -l 32 -n 3 -- 0
^done,asm_insns=[
{address="0x000107bc",func-name="main",offset="0",
inst="save  %sp, -112, %sp"},
{address="0x000107c0",func-name="main",offset="4",
inst="mov  2, %o0"},
{address="0x000107c4",func-name="main",offset="8",
inst="sethi  %hi(0x11800), %o2"}]
(gdb)
```

:::

Disassemble 3 instructions from the start of `main` in mixed mode:

::: smallexample

```bash
(gdb)
-data-disassemble -f basics.c -l 32 -n 3 -- 1
^done,asm_insns=[
src_and_asm_line={line="31",
file="../../../src/gdb/testsuite/gdb.mi/basics.c",
fullname="/absolute/path/to/src/gdb/testsuite/gdb.mi/basics.c",
line_asm_insn=[{address="0x000107bc",
func-name="main",offset="0",inst="save  %sp, -112, %sp"}]},
src_and_asm_line={line="32",
file="../../../src/gdb/testsuite/gdb.mi/basics.c",
fullname="/absolute/path/to/src/gdb/testsuite/gdb.mi/basics.c",
line_asm_insn=[{address="0x000107c0",
func-name="main",offset="4",inst="mov  2, %o0"},
{address="0x000107c4",func-name="main",offset="8",
inst="sethi  %hi(0x11800), %o2"}]}]
(gdb)
```

:::

#### The `-data-evaluate-expression` Command

#### Synopsis

::: smallexample

```bash
 -data-evaluate-expression expr
```

:::


Evaluate `expr` as an expression. The expression could contain an inferior function call. The function call will execute synchronously. If the expression contains spaces, it must be enclosed in double quotes.

> 评估`expr`表达式。表达式可能包含较低级的函数调用。该函数调用将同步执行。如果表达式包含空格，则必须用双引号括起来。

#### [GDB]

The corresponding [GDB]' command.

#### Example


In the following example, the numbers that precede the commands are the *tokens* described in [[GDB/MI] returns the same tokens in its output.

> 在下面的示例中，在命令之前的数字是[[GDB/MI]]在其输出中描述的*标记*。

::: smallexample

```bash
211-data-evaluate-expression A
211^done,value="1"
(gdb)
311-data-evaluate-expression &A
311^done,value="0xefffeb7c"
(gdb)
411-data-evaluate-expression A+3
411^done,value="4"
(gdb)
511-data-evaluate-expression "A + 3"
511^done,value="4"
(gdb)
```

:::

#### The `-data-list-changed-registers` Command

#### Synopsis

::: smallexample

```bash
 -data-list-changed-registers
```

:::

Display a list of the registers that have changed.

#### [GDB]

[GDB]'.

#### Example

On a PPC MBX board:

::: smallexample

```bash
(gdb)
-exec-continue
^running

(gdb)
*stopped,reason="breakpoint-hit",disp="keep",bkptno="1",frame={
func="main",args=,file="try.c",fullname="/home/foo/bar/try.c",
line="5",arch="powerpc"}
(gdb)
-data-list-changed-registers
^done,changed-registers=["0","1","2","4","5","6","7","8","9",
"10","11","13","14","15","16","17","18","19","20","21","22","23",
"24","25","26","27","28","30","31","64","65","66","67","69"]
(gdb)
```

:::

#### The `-data-list-register-names` Command

#### Synopsis

::: smallexample

```bash
 -data-list-register-names [ ( regno )+ ]
```

:::


Show a list of register names for the current target. If no arguments are given, it shows a list of the names of all the registers. If integer numbers are given as arguments, it will print a list of the names of the registers corresponding to the arguments. To ensure consistency between a register name and its number, the output list may include empty register names.

> 显示当前目标的寄存器名称列表。如果没有给出参数，它会显示所有寄存器名称的列表。如果参数是整数，它将打印对应参数的寄存器名称列表。为了确保寄存器名称和其数字之间的一致性，输出列表可能包括空的寄存器名称。

#### [GDB]

[GDB]'.

#### Example

For the PPC MBX board:

::: smallexample

```bash
(gdb)
-data-list-register-names
^done,register-names=["r0","r1","r2","r3","r4","r5","r6","r7",
"r8","r9","r10","r11","r12","r13","r14","r15","r16","r17","r18",
"r19","r20","r21","r22","r23","r24","r25","r26","r27","r28","r29",
"r30","r31","f0","f1","f2","f3","f4","f5","f6","f7","f8","f9",
"f10","f11","f12","f13","f14","f15","f16","f17","f18","f19","f20",
"f21","f22","f23","f24","f25","f26","f27","f28","f29","f30","f31",
"", "pc","ps","cr","lr","ctr","xer"]
(gdb)
-data-list-register-names 1 2 3
^done,register-names=["r1","r2","r3"]
(gdb)
```

:::

#### The `-data-list-register-values` Command

#### Synopsis

::: smallexample

```bash
 -data-list-register-values
    [ --skip-unavailable ] fmt [ ( regno )*]
```

:::


Display the registers' contents. The format according to which the registers' contents are to be returned is given by `fmt`, followed by an optional list of numbers specifying the registers to display. A missing list of numbers indicates that the contents of all the registers must be returned. The `--skip-unavailable` option indicates that only the available registers are to be returned.

> 显示寄存器的内容。返回寄存器内容的格式由`fmt`指定，后面可以跟一个可选的数字列表指定要显示的寄存器。如果没有数字列表，则必须返回所有寄存器的内容。`--skip-unavailable`选项表示只返回可用的寄存器。

Allowed formats for `fmt` are:

`x`

:   Hexadecimal

`o`

:   Octal

`t`

:   Binary

`d`

:   Decimal

`r`

:   Raw

`N`

:   Natural

#### [GDB]

The corresponding [GDB]'.

#### Example


For a PPC MBX board (note: line breaks are for readability only, they don't appear in the actual output):

> 对于PPC MBX板（注意：换行仅用于可读性，实际输出中不会出现）

::: smallexample

```bash
(gdb)
-data-list-register-values r 64 65
^done,register-values=[,
]
(gdb)
-data-list-register-values x
^done,register-values=[,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
,
]
(gdb)
```

:::

#### The `-data-read-memory` Command

This command is deprecated, use `-data-read-memory-bytes` instead.

#### Synopsis

::: smallexample

```bash
 -data-read-memory [ -o byte-offset ]
   address word-format word-size
   nr-rows nr-cols [ aschar ]
```

:::

where:

'`address`'


:   An expression specifying the address of the first memory word to be read. Complex expressions containing embedded white space should be quoted using the C convention.

> 一个指定要读取的第一个内存字地址的表达式。包含嵌入空白的复杂表达式应使用C约定进行引用。

'`word-format`'


:   The format to be used to print the memory words. The notation is the same as for [GDB]'s `print` command (see [Output Formats](Output-Formats.html#Output-Formats)).

> 打印内存单词所使用的格式。该符号与[GDB]的“print”命令相同（请参见[输出格式](Output-Formats.html#Output-Formats)）。

'`word-size`'

:   The size of each memory word in bytes.

'`nr-rows`'

:   The number of rows in the output table.

'`nr-cols`'

:   The number of columns in the output table.

'`aschar`'


:   If present, indicates that each row should include an [ASCII] characters are those whose code is between 32 and 126, inclusively).

> 如果存在，表示每行都应包括一个[ASCII]字符（其代码介于32和126之间，包括32和126）。

'`byte-offset`'

:   An offset to add to the `address` before fetching memory.

This command displays memory contents as a table of `nr-rows`'.


The address of the next/previous row or page is available in '`next-row`'.

> 下一行/上一行或页面的地址可在 'next-row' 中找到。

#### [GDB]

The corresponding [GDB]' memory read command.

#### Example


Read six bytes of memory starting at `bytes+6` but then offset by `-6` bytes. Format as three rows of two columns. One byte per word. Display each word in hex.

> 从`bytes+6`开始读取6个字节的内存，但偏移-6个字节。以三行两列的格式显示，每个字一个字节，以十六进制显示每个字。

::: smallexample

```bash
(gdb)
9-data-read-memory -o -6 -- bytes+6 x 1 3 2
9^done,addr="0x00001390",nr-bytes="6",total-bytes="6",
next-row="0x00001396",prev-row="0x0000138e",next-page="0x00001396",
prev-page="0x0000138a",memory=[
,
,
]
(gdb)
```

:::


Read two bytes of memory starting at address `shorts + 64` and display as a single word formatted in decimal.

> 从地址shorts + 64开始读取两个字节的内存，并以十进制的形式显示为一个单词。

::: smallexample

```bash
(gdb)
5-data-read-memory shorts+64 d 2 1 1
5^done,addr="0x00001510",nr-bytes="2",total-bytes="2",
next-row="0x00001512",prev-row="0x0000150e",
next-page="0x00001512",prev-page="0x0000150e",memory=[
]
(gdb)
```

:::


Read thirty two bytes of memory starting at `bytes+16` and format as eight rows of four columns. Include a string encoding with '`x`' used as the non-printable character.

> 从`bytes+16`开始，读取32个字节的内存，按8行4列格式化。使用'`x`'作为不可打印字符，包含字符串编码。

::: smallexample

```bash
(gdb)
4-data-read-memory bytes+16 x 1 8 4 x
4^done,addr="0x000013a0",nr-bytes="32",total-bytes="32",
next-row="0x000013c0",prev-row="0x0000139c",
next-page="0x000013c0",prev-page="0x00001380",memory=[
,
,
,
,
,
,
,
]
(gdb)
```

:::

#### The `-data-read-memory-bytes` Command

#### Synopsis

::: smallexample

```bash
 -data-read-memory-bytes [ -o offset ]
   address count
```

:::

where:

'`address`'


:   An expression specifying the address of the first addressable memory unit to be read. Complex expressions containing embedded white space should be quoted using the C convention.

> 一个表达式指定要读取的第一个可寻址的内存单元的地址。包含嵌入空格的复杂表达式应使用C约定进行引用。

'`count`'


:   The number of addressable memory units to read. This should be an integer literal.

> 这应该是一个整数文字，表示可读取的内存单元的数量。

'`offset`'


:   The offset relative to `address` at which to start reading. This should be an integer literal. This option is provided so that a frontend is not required to first evaluate address and then perform address arithmetics itself.

> 相对于`地址`开始读取的偏移量。这应该是一个整数字面量。为了避免前端首先评估地址，然后自行执行地址算术，提供了此选项。


This command attempts to read all accessible memory regions in the specified range. First, all regions marked as unreadable in the memory map (if one is defined) will be skipped. See [Memory Region Attributes](Memory-Region-Attributes.html#Memory-Region-Attributes). Second, [GDB] will try to read a subset of the region.

> 此命令尝试读取指定范围内的所有可访问内存区域。首先，将跳过内存映射中标记为不可读的所有区域（如果定义了）。参见[内存区域属性](Memory-Region-Attributes.html#Memory-Region-Attributes)。其次，[GDB]将尝试读取该区域的子集。


In general, every single memory unit in the region may be readable or not, and the only way to read every readable unit is to try a read at every address, which is not practical. Therefore, [GDB] will not read it.

> 一般来说，该地区的每一个存储单元可能是可读的，也可能是不可读的，而唯一读取可读单元的方式就是在每个地址试图读取，这并不实用。因此，[GDB]不会读取它。


The result record (see [GDB/MI Result Records](GDB_002fMI-Result-Records.html#GDB_002fMI-Result-Records)) that is output of the command includes a field named '`memory`' whose content is a list of tuples. Each tuple represent a successfully read memory block and has the following fields:

> 结果记录（参见[GDB/MI结果记录](GDB_002fMI-Result-Records.html#GDB_002fMI-Result-Records))，该命令的输出包含一个名为“memory”的字段，其内容为一个元组列表。每个元组表示一个成功读取的内存块，其具有以下字段：

`begin`

:   The start address of the memory block, as hexadecimal literal.

`end`

:   The end address of the memory block, as hexadecimal literal.

`offset`


:   The offset of the memory block, as hexadecimal literal, relative to the start address passed to `-data-read-memory-bytes`.

> 十六进制文字相对于传递给`-data-read-memory-bytes`的起始地址的内存块偏移量。

`contents`

:   The contents of the memory block, in hex.

#### [GDB]

The corresponding [GDB]'.

#### Example

::: smallexample

```bash
(gdb)
-data-read-memory-bytes &a 10
^done,memory=[{begin="0xbffff154",offset="0x00000000",
              end="0xbffff15e",
              contents="01000000020000000300"}]
(gdb)
```

:::

#### The `-data-write-memory-bytes` Command

#### Synopsis

::: smallexample

```bash
 -data-write-memory-bytes address contents
 -data-write-memory-bytes address contents [count]
```

:::

where:

'`address`'


:   An expression specifying the address of the first addressable memory unit to be written. Complex expressions containing embedded white space should be quoted using the C convention.

> 一个表达式指定要写入的第一个可寻址的存储单元的地址。使用C约定，应该用引号引用包含嵌入空格的复杂表达式。

'`contents`'


:   The hex-encoded data to write. It is an error if `contents` does not represent an integral number of addressable memory units.

> 要写入的十六进制编码数据。如果`contents`不表示可寻址存储单元的整数，则会出现错误。

'`count`'


:   Optional argument indicating the number of addressable memory units to be written. If `count` memory units.

> 指示要写入的可寻址存储单元数量的可选参数。如果`count`存储单元。

#### [GDB]

There's no corresponding [GDB] command.

#### Example

::: smallexample

```bash
(gdb)
-data-write-memory-bytes &a "aabbccdd"
^done
(gdb)
```

:::

::: smallexample

```bash
(gdb)
-data-write-memory-bytes &a "aabbccdd" 16e
^done
(gdb)
```

:::

---

::: header
Next: [GDB/MI Tracepoint Commands](GDB_002fMI-Tracepoint-Commands.html#GDB_002fMI-Tracepoint-Commands)]
:::
