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

Note that only 64-bit applications can use ADI and need to be built with ADI-enabled.

Values of the ADI version tags, which are in granularity of a cacheline (64 bytes), can be viewed or modified.

`adi (examine | x) [ / n ] addr`

The `adi examine` command displays the value of one ADI version tag per cacheline.

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

`n` is a decimal integer specifying the number in bytes; the default is 1. It specifies how much ADI version information, at the ratio of 1:ADI block size, to modify.

`addr` to begin modifying the ADI version tags.

`tag` is the new ADI version tag.

For example, do the following to modify then verify ADI versions of variable \"shmaddr\":

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
