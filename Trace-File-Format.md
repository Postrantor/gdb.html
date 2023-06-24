---
tip: translate by openai@2023-06-24 04:03:47
...
---
description: Trace File Format (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Trace File Format (Debugging with GDB)
lang: en
resource-type: document
title: Trace File Format (Debugging with GDB)
---
::: header
Next: [Index Section Format](Index-Section-Format.html#Index-Section-Format)]
:::

---

## Appendix I Trace File Format


The trace file comes in three parts: a header, a textual description section, and a trace frame section with binary data.

> 跟踪文件分为三部分：头部，文本描述部分和具有二进制数据的跟踪帧部分。


The header has the form `\x7fTRACE0\n`. The first byte is `0x7f` so as to indicate that the file contains binary data, while the `0` is a version number that may have different values in the future.

> 头部的格式是`\x7fTRACE0\n`。第一个字节是`0x7f`，表明文件包含二进制数据，而`0`是可能在未来有不同值的版本号。


The description section consists of multiple lines of [ASCII] will ignore any line that it does not recognize. An empty line marks the end of this section.

> 描述部分包括多行[ASCII]，会忽略任何它无法识别的行。空行标志着这一部分的结束。

`R size`


:   Specifies the size of a register block in bytes. This is equal to the size of a `g` packet payload in the remote protocol. `size` is an ascii decimal number. There should be only one such line in a single trace file.

> 指定寄存器块的大小，以字节为单位。这等于远程协议中的`g`数据包负载的大小。`size`是一个ASCII十进制数字。在单个跟踪文件中只能有一行此类内容。

`status status`


:   Trace status. `status` has the same format as a `qTStatus` remote packet reply. There should be only one such line in a single trace file.

> 跟踪状态。`status`的格式与`qTStatus`远程数据包回复相同。在单个跟踪文件中只应有一行此类内容。

`tp payload`


:   Tracepoint definition. The `payload` has the same format as `qTfP`/`qTsP` remote packet reply payload. A single tracepoint may take multiple lines of definition, corresponding to the multiple reply packets.

> 定义跟踪点。`payload`具有与`qTfP`/`qTsP`远程数据包回复`payload`相同的格式。单个跟踪点可能需要多行定义，对应于多个回复数据包。

`tsv payload`


:   Trace state variable definition. The `payload` has the same format as `qTfV`/`qTsV` remote packet reply payload. A single variable may take multiple lines of definition, corresponding to the multiple reply packets.

> 跟踪状态变量定义。`payload`与`qTfV`/`qTsV`远程数据包回复`payload`具有相同的格式。单个变量可以占用多行定义，对应于多个回复数据包。

`tdesc payload`


:   Target description in XML format. The `payload` is a single line of the XML file. All such lines should be concatenated together to get the original XML file. This file is in the same format as `qXfer` `features` payload, and corresponds to the main `target.xml` file. Includes are not allowed.

> XML格式的目标描述。`payload`是XML文件的单行。所有这样的行应该连接在一起以获得原始的XML文件。此文件与`qXfer` `features` payload的格式相同，并且对应于主`target.xml`文件。不允许包含。


The trace frame section consists of a number of consecutive frames. Each frame begins with a two-byte tracepoint number, followed by a four-byte size giving the amount of data in the frame. The data in the frame consists of a number of blocks, each introduced by a character indicating its type (at least register, memory, and trace state variable). The data in this section is raw binary, not a hexadecimal or other encoding; its endianness matches the target's endianness.

> 这个跟踪框架部分由一系列连续的帧组成。每个帧以两个字节的跟踪点号开头，后面跟着四个字节的大小，表示帧中数据的量。帧中的数据由若干块组成，每块都由一个字符来表示它的类型（至少有寄存器、内存和跟踪状态变量）。该部分的数据是原始二进制数据，而不是十六进制或其他编码；它的字节序与目标的字节序相匹配。

`R bytes`


:   Register block. The number and ordering of bytes matches that of a `g` packet in the remote protocol. Note that these are the actual bytes, in target order, not a hexadecimal encoding.

> 注册块。字节的数量和顺序与远程协议中的'g'数据包相匹配。请注意，这些是实际字节，按目标顺序而不是十六进制编码。

`M address length bytes...`


:   Memory block. This is a contiguous block of memory, at the 8-byte address `address` bytes.

> 这是一块连续的内存块，地址为`address`字节的8字节地址。

`V number value`


:   Trace state variable block. This records the 8-byte signed value `value`.

> 跟踪状态变量块。这记录8字节有符号值“value”。


Future enhancements of the trace file format may include additional types of blocks.

> 未来的跟踪文件格式可能会包括更多类型的块。

---

::: header
Next: [Index Section Format](Index-Section-Format.html#Index-Section-Format)]
:::
