---
tip: translate by openai@2023-06-23 20:44:10
...
---
description: Dump/Restore Files (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Dump/Restore Files (Debugging with GDB)
lang: en
resource-type: document
title: Dump/Restore Files (Debugging with GDB)
---
::: header
Next: [Core File Generation](Core-File-Generation.html#Core-File-Generation)]
:::

---

### 10.19 Copy Between Memory and a File


You can use the commands `dump`, `append`, and `restore` to copy data between target memory and a file. The `dump` and `append` commands write data to a file, and the `restore` command reads data from a file back into the inferior's memory. Files may be in binary, Motorola S-record, Intel hex, Tektronix Hex, or Verilog Hex format; however, [GDB] can only append to binary files, and cannot read from Verilog Hex files.

> 你可以使用命令`dump`、`append`和`restore`在目标内存和文件之间复制数据。`dump`和`append`命令将数据写入文件，而`restore`命令将数据从文件读取回到被检查的内存中。文件可以是二进制、Motorola S-record、Intel hex、Tektronix Hex或Verilog Hex格式；但是，[GDB]只能追加到二进制文件，不能读取Verilog Hex文件。

`dump [format] memory filename start_addr end_addr`

`dump [format] value filename expr`

Dump the contents of memory from `start_addr` in the given format.

The `format` parameter may be any one of:

`binary`

:   Raw binary form.

`ihex`

:   Intel hex format.

`srec`

:   Motorola S-record format.

`tekhex`

:   Tektronix Hex format.

`verilog`

:   Verilog Hex format.

[GDB] dumps the data in raw binary form.

`append [binary] memory filename start_addr end_addr`

`append [binary] value filename expr`


Append the contents of memory from `start_addr` can only append data to files in raw binary form.)

> 从`start_addr`开始，只能将内存的内容以原始二进制格式附加到文件中。

`restore filename [binary] bias start end`


Restore the contents of file `filename` file format, except for raw binary. To restore a raw binary file you must specify the optional keyword `binary` after the filename.

> 恢复文件`filename`的内容，除了原始二进制文件。要恢复原始二进制文件，必须在文件名之后指定可选关键字`binary`。

If `bias` from that location.

If `start` argument is applied.

---

::: header
Next: [Core File Generation](Core-File-Generation.html#Core-File-Generation)]
:::
