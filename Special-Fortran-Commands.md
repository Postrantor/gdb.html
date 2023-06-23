---
tip: translate by openai@2023-06-23 13:25:19
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

> [GDB]有一些命令可以支持Fortran特定功能，比如显示公共块。

`info common [common-name]`


This command prints the values contained in the Fortran `COMMON` block whose name is `common-name`

> 这个命令打印出Fortran `COMMON` 块中名为`common-name`的值。

`set fortran repack-array-slices [on|off]`

`show fortran repack-array-slices`


When taking a slice from an array, a Fortran compiler can choose to either produce an array descriptor that describes the slice in place, or it may repack the slice, copying the elements of the slice into a new region of memory.

> 当从数组中取出一片时，Fortran编译器可以选择生成一个描述片段的数组描述符，或者将片段重新打包，将片段的元素复制到新的内存区域。


When this setting is on, then [GDB] will create array descriptors for slices that reference the original data in place.

> 当设置开启时，GDB将为引用原始数据的切片创建数组描述符。


[GDB] will never repack an array slice if the data for the slice is contiguous within the original array.

> GDB不会重新封装数组切片，如果切片的数据在原始数组中是连续的。


[GDB] does not support printing non-contiguous strings.

> [GDB]不支持打印非连续的字符串。


The default for this setting is `off`.

> 默认设置为关闭。
