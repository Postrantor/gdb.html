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

`restore filename [binary] bias start end`

Restore the contents of file `filename` file format, except for raw binary. To restore a raw binary file you must specify the optional keyword `binary` after the filename.

If `bias` from that location.

If `start` argument is applied.

---

::: header
Next: [Core File Generation](Core-File-Generation.html#Core-File-Generation)]
:::
