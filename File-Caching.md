---
description: File Caching (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: File Caching (Debugging with GDB)
lang: en
resource-type: document
title: File Caching (Debugging with GDB)
---
::: header
Next: [Separate Debug Files](Separate-Debug-Files.html#Separate-Debug-Files)]
:::

---

### 18.2 File Caching

To speed up file loading, and reduce memory usage, [GDB] will reuse the `bfd` objects used to track open files. See [BFD](http://sourceware.org/binutils/docs/bfd/index.html#Top) in The Binary File Descriptor Library. The following commands allow visibility and control of the caching behavior.

`maint info bfds`

This prints information about each `bfd` object that is known to [GDB].

`maint set bfd-sharing`

`maint show bfd-sharing`

Control whether `bfd` objects can be shared. When sharing is enabled [GDB] reuses already open `bfd` objects rather than reopening the same file. Turning sharing off does not cause already shared `bfd` objects to be unshared, but all future files that are opened will create a new `bfd` object. Similarly, re-enabling sharing does not cause multiple existing `bfd` objects to be collapsed into a single shared `bfd` object.

`set debug bfd-cache level`

Turns on debugging of the bfd cache, setting the level to `level`.

`show debug bfd-cache`

Show the current debugging level of the bfd cache.
