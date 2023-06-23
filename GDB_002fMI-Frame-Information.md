---
description: GDB/MI Frame Information (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Frame Information (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Frame Information (Debugging with GDB)
---
::: header
Next: [GDB/MI Thread Information](GDB_002fMI-Thread-Information.html#GDB_002fMI-Thread-Information)]
:::

---

#### 27.5.5 [GDB/MI]

Response from many MI commands includes an information about stack frame. This information is a tuple that may have the following fields:

`level`

:   The level of the stack frame. The innermost frame has the level of zero. This field is always present.

`func`

:   The name of the function corresponding to the frame. This field may be absent if [GDB] is unable to determine the function name.

`addr`

:   The code address for the frame. This field is always present.

`addr_flags`

:   Optional field containing any flags related to the address. These flags are architecture-dependent; see [Architectures](Architectures.html#Architectures) for their meaning for a particular CPU.

`file`

:   The name of the source files that correspond to the frame's code address. This field may be absent.

`line`

:   The source line corresponding to the frames' code address. This field may be absent.

`from`

:   The name of the binary file (either executable or shared library) the corresponds to the frame's code address. This field may be absent.
