---
tip: translate by openai@2023-06-23 13:24:36
...
---
description: Sparc64 (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Sparc64 (Debugging with GDB)
lang: en
resource-type: document
title: Sparc64 (Debugging with GDB)
-----------------------------------

::: header
Next: [S12Z](S12Z.html#S12Z)]
:::

---

#### 21.4.8 Sparc64

#### 21.4.8.1 ADI Support

The M7 processor supports an Application Data Integrity (ADI) feature that detects invalid data accesses. When software allocates memory and enables ADI on the allocated memory, it chooses a 4-bit version number, sets the version in the upper 4 bits of the 64-bit pointer to that data, and stores the 4-bit version in every cacheline of that data. Hardware saves the latter in spare bits in the cache and memory hierarchy. On each load and store, the processor compares the upper 4 VA (virtual address) bits to the cacheline's version. If there is a mismatch, the processor generates a version mismatch trap which can be either precise or disrupting. The trap is an error condition which the kernel delivers to the process as a SIGSEGV signal.

> 处理器 M7 支持应用程序数据完整性（ADI）功能，用于检测无效数据访问。当软件分配内存并在分配的内存上启用 ADI 时，它会选择一个 4 位版本号，将版本号设置在 64 位指针的前 4 位，并将这 4 位版本号存储在该数据的每个缓存行中。硬件会将后者存储在缓存和内存层次结构中的备用位中。在每次加载和存储时，处理器都会将前 4 个 VA（虚拟地址）位与缓存行的版本进行比较。如果存在不匹配，处理器将生成版本不匹配中断，该中断可以是精确的或中断的。该中断是内核将错误条件传递给进程的 SIGSEGV 信号。

Note that only 64-bit applications can use ADI and need to be built with ADI-enabled.

Values of the ADI version tags, which are in granularity of a cacheline (64 bytes), can be viewed or modified.

> 可以查看或修改以缓存行（64 字节）粒度的 ADI 版本标签的值。

`adi (examine | x) [ / n ] addr`

The `adi examine` command displays the value of one ADI version tag per cacheline.

> 命令 `adi examine` 将每个缓存行显示一个 ADI 版本标签的值。

`n` is a decimal integer specifying the number in bytes; the default is 1. It specifies how much ADI version information, at the ratio of 1:ADI block size, to display.

`addr` to begin displaying the ADI version tags.

Below is an example of displaying ADI versions of variable \"shmaddr\".

> 以下是变量 "shmaddr" 的 ADI 版本的显示示例。

::: smallexample

```bash
(gdb) adi x/100 shmaddr
   0xfff800010002c000:     0 0
```

:::

`adi (assign | a) [ / n ] addr = tag`

The `adi assign` command is used to assign new ADI version tag to an address.

> 命令 `adi assign` 用于为地址分配新的 ADI 版本标签。

`n` is a decimal integer specifying the number in bytes; the default is 1. It specifies how much ADI version information, at the ratio of 1:ADI block size, to modify.

`addr` to begin modifying the ADI version tags.

`tag` is the new ADI version tag.

For example, do the following to modify then verify ADI versions of variable \"shmaddr\":

> 例如，要修改然后验证变量“shmaddr”的 ADI 版本，请按照以下步骤操作：

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
