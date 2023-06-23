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

`info common [common-name]`

This command prints the values contained in the Fortran `COMMON` block whose name is `common-name`

`set fortran repack-array-slices [on|off]`

`show fortran repack-array-slices`

When taking a slice from an array, a Fortran compiler can choose to either produce an array descriptor that describes the slice in place, or it may repack the slice, copying the elements of the slice into a new region of memory.

When this setting is on, then [GDB] will create array descriptors for slices that reference the original data in place.

[GDB] will never repack an array slice if the data for the slice is contiguous within the original array.

[GDB] does not support printing non-contiguous strings.

The default for this setting is `off`.
