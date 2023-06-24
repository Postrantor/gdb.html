---
tip: translate by openai@2023-06-24 03:05:46
...
---
description: Sparc64 (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Sparc64 (Debugging with GDB)
lang: en
resource-type: document
title: Sparc64 (Debugging with GDB)
---
::: header
Next: [S12Z](S12Z.html#S12Z)]
:::

---

#### 21.4.8 Sparc64

#### 21.4.8.1 ADI Support


The M7 processor supports an Application Data Integrity (ADI) feature that detects invalid data accesses. When software allocates memory and enables ADI on the allocated memory, it chooses a 4-bit version number, sets the version in the upper 4 bits of the 64-bit pointer to that data, and stores the 4-bit version in every cacheline of that data. Hardware saves the latter in spare bits in the cache and memory hierarchy. On each load and store, the processor compares the upper 4 VA (virtual address) bits to the cacheline's version. If there is a mismatch, the processor generates a version mismatch trap which can be either precise or disrupting. The trap is an error condition which the kernel delivers to the process as a SIGSEGV signal.

> 处理器M7支持应用数据完整性（ADI）功能，用于检测无效数据访问。当软件分配内存并在分配的内存上启用ADI时，它会选择一个4位版本号，将该版本号设置在64位指针的前4位，并将4位版本号存储在该数据的每个缓存行中。硬件将后者存储在缓存和内存层次结构的备用位中。在每次加载和存储时，处理器将上4个VA（虚拟地址）位与缓存行的版本进行比较。如果有不匹配，处理器将生成一个版本不匹配的陷阱，该陷阱可以是精确的或中断的。该陷阱是内核将错误条件传递给进程作为SIGSEGV信号的错误条件。


Note that only 64-bit applications can use ADI and need to be built with ADI-enabled.

> 只有64位应用程序可以使用ADI，并且需要使用ADI构建。


Values of the ADI version tags, which are in granularity of a cacheline (64 bytes), can be viewed or modified.

> 可以查看或修改ADI版本标签的值，这些值的粒度为缓存行（64字节）。

`adi (examine | x) [ / n ] addr`


The `adi examine` command displays the value of one ADI version tag per cacheline.

> 命令`adi examine`会显示每个缓存行的一个ADI版本标记的值。

`n` is a decimal integer specifying the number in bytes; the default is 1. It specifies how much ADI version information, at the ratio of 1:ADI block size, to display.

`addr` to begin displaying the ADI version tags.

Below is an example of displaying ADI versions of variable \"shmaddr\".

::: smallexample

```bash
(gdb) adi x/100 shmaddr
   0xfff800010002c000:     0 0
```

:::

`adi (assign | a) [ / n ] addr = tag`


The `adi assign` command is used to assign new ADI version tag to an address.

> 命令`adi assign`用于为地址分配新的ADI版本标签。

`n` is a decimal integer specifying the number in bytes; the default is 1. It specifies how much ADI version information, at the ratio of 1:ADI block size, to modify.

`addr` to begin modifying the ADI version tags.

`tag` is the new ADI version tag.


For example, do the following to modify then verify ADI versions of variable \"shmaddr\":

> 例如，要修改并校验变量"shmaddr"的ADI版本，请执行以下操作：

::: smallexample

```bash
(gdb) adi a/100 shmaddr = 7
(gdb) adi x/100 shmaddr
   0xfff800010002c000:     7 7
```

:::

---

::: header
Next: [S12Z](S12Z.html#S12Z)]
:::
