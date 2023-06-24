---
tip: translate by openai@2023-06-23 21:00:45
...
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

> 为了加快文件加载速度，减少内存使用，[GDB]将重用用于跟踪打开文件的`bfd`对象。请参阅The Binary File Descriptor Library中的[BFD](http://sourceware.org/binutils/docs/bfd/index.html#Top)。以下命令允许可见性和控制缓存行为。

`maint info bfds`

This prints information about each `bfd` object that is known to [GDB].

`maint set bfd-sharing`

`maint show bfd-sharing`


Control whether `bfd` objects can be shared. When sharing is enabled [GDB] reuses already open `bfd` objects rather than reopening the same file. Turning sharing off does not cause already shared `bfd` objects to be unshared, but all future files that are opened will create a new `bfd` object. Similarly, re-enabling sharing does not cause multiple existing `bfd` objects to be collapsed into a single shared `bfd` object.

> 控制`bfd`对象是否可以共享。当启用共享时，[GDB]会重用已经打开的`bfd`对象，而不是重新打开同一个文件。关闭共享不会导致已经共享的`bfd`对象被取消共享，但是所有未来打开的文件将创建一个新的`bfd`对象。同样，重新启用共享也不会导致多个现有的`bfd`对象合并为单个共享的`bfd`对象。

`set debug bfd-cache level`

Turns on debugging of the bfd cache, setting the level to `level`.

`show debug bfd-cache`

Show the current debugging level of the bfd cache.
