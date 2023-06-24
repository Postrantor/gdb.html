---
tip: translate by openai@2023-06-23 23:13:33
...
---
description: i386 Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: i386 Features (Debugging with GDB)
lang: en
resource-type: document
title: i386 Features (Debugging with GDB)
---
::: header
Next: [LoongArch Features](LoongArch-Features.html#LoongArch-Features)]
:::

---

#### G.5.4 i386 Features


The '`org.gnu.gdb.i386.core`' feature is required for i386/amd64 targets. It should describe the following registers:

> 针对i386/amd64目标，需要'org.gnu.gdb.i386.core'功能。它应该描述以下寄存器：

- \- '`eax`' for i386
- \- '`rax`' for amd64
- \- '`eflags`'
- \- '`st0`'
- \- '`fctrl`'

The register sets may be different, depending on the target.


The '`org.gnu.gdb.i386.sse`' feature is optional. It should describe registers:

> 'org.gnu.gdb.i386.sse'功能是可选的。它应该描述寄存器。

- \- '`xmm0`' for i386
- \- '`xmm0`' for amd64
- \- '`mxcsr`'

The '`org.gnu.gdb.i386.avx` registers:

- \- '`ymm0h`' for i386
- \- '`ymm0h`' for amd64


The '`org.gnu.gdb.i386.mpx`' is an optional feature representing Intel Memory Protection Extension (MPX). It should describe the following registers:

> `org.gnu.gdb.i386.mpx` 是一项可选功能，代表Intel Memory Protection Extension（MPX）。它应该描述以下寄存器：

- \- '`bnd0raw`' for i386 and amd64.
- \- '`bndcfgu`' for i386 and amd64.

The '`org.gnu.gdb.i386.linux`'.

The '`org.gnu.gdb.i386.segments`'.

The '`org.gnu.gdb.i386.avx512` registers:

- \- '`xmm16h`', only valid for amd64.

It should describe the upper 128 bits of additional [YMM] registers:

- \- '`ymm16h`', only valid for amd64.

It should describe the upper 256 bits of [ZMM] registers:

- \- '`zmm0h`' for i386.
- \- '`zmm0h`' for amd64.

It should describe the additional [ZMM] registers:

- \- '`zmm16h`', only valid for amd64.


The '`org.gnu.gdb.i386.pkeys`'. It is a 32-bit register valid for i386 and amd64.

> 这是一个32位的i386和amd64有效的寄存器，名为org.gnu.gdb.i386.pkeys。

---

::: header
Next: [LoongArch Features](LoongArch-Features.html#LoongArch-Features)]
:::
