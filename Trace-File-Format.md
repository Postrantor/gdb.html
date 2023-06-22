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

The header has the form `\x7fTRACE0\n`. The first byte is `0x7f` so as to indicate that the file contains binary data, while the `0` is a version number that may have different values in the future.

The description section consists of multiple lines of [ASCII] will ignore any line that it does not recognize. An empty line marks the end of this section.

`R size`

:   Specifies the size of a register block in bytes. This is equal to the size of a `g` packet payload in the remote protocol. `size` is an ascii decimal number. There should be only one such line in a single trace file.

`status status`

:   Trace status. `status` has the same format as a `qTStatus` remote packet reply. There should be only one such line in a single trace file.

`tp payload`

:   Tracepoint definition. The `payload` has the same format as `qTfP`/`qTsP` remote packet reply payload. A single tracepoint may take multiple lines of definition, corresponding to the multiple reply packets.

`tsv payload`

:   Trace state variable definition. The `payload` has the same format as `qTfV`/`qTsV` remote packet reply payload. A single variable may take multiple lines of definition, corresponding to the multiple reply packets.

`tdesc payload`

:   Target description in XML format. The `payload` is a single line of the XML file. All such lines should be concatenated together to get the original XML file. This file is in the same format as `qXfer` `features` payload, and corresponds to the main `target.xml` file. Includes are not allowed.

The trace frame section consists of a number of consecutive frames. Each frame begins with a two-byte tracepoint number, followed by a four-byte size giving the amount of data in the frame. The data in the frame consists of a number of blocks, each introduced by a character indicating its type (at least register, memory, and trace state variable). The data in this section is raw binary, not a hexadecimal or other encoding; its endianness matches the target's endianness.

`R bytes`

:   Register block. The number and ordering of bytes matches that of a `g` packet in the remote protocol. Note that these are the actual bytes, in target order, not a hexadecimal encoding.

`M address length bytes...`

:   Memory block. This is a contiguous block of memory, at the 8-byte address `address` bytes.

`V number value`

:   Trace state variable block. This records the 8-byte signed value `value`.

Future enhancements of the trace file format may include additional types of blocks.

---

::: header
Next: [Index Section Format](Index-Section-Format.html#Index-Section-Format)]
:::
