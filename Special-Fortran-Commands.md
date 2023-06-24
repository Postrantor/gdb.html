---
tip: translate by openai@2023-06-24 03:06:25
...
---
description: Special Fortran Commands (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Special Fortran Commands (Debugging with GDB)
lang: en
resource-type: document
title: Special Fortran Commands (Debugging with GDB)
---
::: header
Previous: [Fortran Intrinsics](Fortran-Intrinsics.html#Fortran-Intrinsics)]
:::

---

#### 15.4.6.4 Special Fortran Commands


[GDB] has some commands to support Fortran-specific features, such as displaying common blocks.

> [GDB]有一些命令来支持Fortran特定的功能，比如显示公共块。

`info common [common-name]`


This command prints the values contained in the Fortran `COMMON` block whose name is `common-name`

> 这个命令打印出Fortran `COMMON` 块中名为`common-name`的值。

`set fortran repack-array-slices [on|off]`

`show fortran repack-array-slices`


When taking a slice from an array, a Fortran compiler can choose to either produce an array descriptor that describes the slice in place, or it may repack the slice, copying the elements of the slice into a new region of memory.

> 当从数组中取出一片时，Fortran编译器可以选择生成描述该片的数组描述符，或者可以重新打包该片，将片中的元素复制到新的内存区域中。


When this setting is on, then [GDB] will create array descriptors for slices that reference the original data in place.

> 当这个设置打开时，GDB将为引用原始数据的切片创建数组描述符。


[GDB] will never repack an array slice if the data for the slice is contiguous within the original array.

> GDB不会重新打包原始数组中连续的数据的数组片段。

[GDB] does not support printing non-contiguous strings.

The default for this setting is `off`.
