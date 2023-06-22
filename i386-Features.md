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

- \- '`eax`' for i386
- \- '`rax`' for amd64
- \- '`eflags`'
- \- '`st0`'
- \- '`fctrl`'

The register sets may be different, depending on the target.

The '`org.gnu.gdb.i386.sse`' feature is optional. It should describe registers:

- \- '`xmm0`' for i386
- \- '`xmm0`' for amd64
- \- '`mxcsr`'

The '`org.gnu.gdb.i386.avx` registers:

- \- '`ymm0h`' for i386
- \- '`ymm0h`' for amd64

The '`org.gnu.gdb.i386.mpx`' is an optional feature representing Intel Memory Protection Extension (MPX). It should describe the following registers:

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

---

::: header
Next: [LoongArch Features](LoongArch-Features.html#LoongArch-Features)]
:::
