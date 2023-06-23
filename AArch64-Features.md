---
description: AArch64 Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: AArch64 Features (Debugging with GDB)
lang: en
resource-type: document
title: AArch64 Features (Debugging with GDB)
---
::: header
Next: [ARC Features](ARC-Features.html#ARC-Features)]
:::

---

#### G.5.1 AArch64 Features

#### G.5.1.1 AArch64 core registers feature

The '`org.gnu.gdb.aarch64.core`' feature is required for AArch64 targets. It must contain the following:

- \- '`x0`'.
- \- '`sp`'.
- \- '`pc`'.
- \- '`cpsr`', the current program status register. It is 32 bits in size and has a custom flags type.

The semantics of the individual flags and fields in '`cpsr`' can change as new architectural features are added. The current layout can be found in the aarch64-core.xml file.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.1.2 AArch64 floating-point registers feature

The '`org.gnu.gdb.aarch64.fpu`' feature is optional. If present, it must contain the following registers:

- \- '`v0`', the vector registers with size of 128 bits. The type is a custom vector type.
- \- '`fpsr`', the floating-point status register. It is 32 bits in size and has a custom flags type.
- \- '`fpcr`', the floating-point control register. It is 32 bits in size and has a custom flags type.

The semantics of the individual flags and fields in '`fpsr`' can change as new architectural features are added.

The types for the vector registers, '`fpsr`' registers can be found in the aarch64-fpu.xml file.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.1.3 AArch64 SVE registers feature

The '`org.gnu.gdb.aarch64.sve`' feature is optional. If present, it means the target supports the Scalable Vector Extension and must contain the following registers:

- \- '`z0`', the scalable vector registers. Their sizes are variable and a multiple of 128 bits up to a maximum of 2048 bit. Their type is a custom union type that helps visualize different sizes of sub-vectors.
- \- '`fpsr`', the floating-point status register. It is 32 bits in size and has a custom flags type.
- \- '`fpcr`', the floating-point control register. It is 32 bits in size and has a custom flags type.
- \- '`p0`', the predicate registers. Their sizes are variable, based on the current vector length, and a multiple of 16 bits. Their types are a custom union to help visualize sub-elements.
- \- '`ffr`', the First Fault register. It has a variable size based on the current vector length and is a multiple of 16 bits. The type is the same as the predicate registers.
- \- '`vg`'.

When [GDB]'.

[GDB]' feature.

The first 128 bits of the '`z`' registers, so changing one will trigger a change to the other.

For the types of the '`z`' registers, please check the aarch64-sve.c file. No XML file is available for this feature because it is dynamically generated based on the current vector length.

The semantics of the individual flags and fields in '`fpsr`' can change as new architectural features are added.

The types for the '`fpsr`' registers can be found in the aarch64-sve.c file, and should match what is described in aarch64-fpu.xml.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.1.4 AArch64 Pointer Authentication registers feature

The '`org.gnu.gdb.aarch64.pauth` could detect support for the Pointer Authentication extension. If present, it must contain one of two possible register sets.

Pointer Authentication masks for user-mode:

- \- '`pauth_dmask`', the user-mode pointer authentication mask for data pointers. It is 64 bits in size.
- \- '`pauth_cmask`', the user-mode pointer authentication mask for code pointers. It is 64 bits in size.

Pointer Authentication masks for user-mode and kernel-mode:

- \- '`pauth_dmask`', the user-mode pointer authentication mask for data pointers. It is 64 bits in size.
- \- '`pauth_cmask`', the user-mode pointer authentication mask for code pointers. It is 64 bits in size.
- \- '`pauth_dmask_high`', the kernel-mode pointer authentication mask for data pointers. It is 64 bits in size.
- \- '`pauth_cmask_high`', the kernel-mode pointer authentication mask for code pointers. It is 64 bits in size.

If [GDB]' marker alongside a function that has a signed link register value that needs to be unmasked/decoded.

[GDB] will also use the masks to remove non-address bits from pointers.

Extra registers are allowed in this feature, but they will not affect [GDB].

Please note the '`org.gnu.gdb.aarch64.pauth`' feature string instead.

The '`org.gnu.gdb.aarch64.pauth_v2`'.

The reason for having feature '`org.gnu.gdb.aarch64.pauth_v2`. This is more common when using emulators and on bare-metal debugging scenarios.

It can also happen if a newer gdbserver is used with an old [GDB] does not know about, potentially leading to a crash.

#### G.5.1.5 AArch64 TLS registers feature

The '`org.gnu.gdb.aarch64.tls`. If present, it must contain either one of the following register sets.

Only '`tpidr`':

- \- '`tpidr`'.

Both '`tpidr`'.

- \- '`tpidr`'.
- \- '`tpidr2`'. It may be used in the future alongside the Scalable Matrix Extension for a lazy restore scheme.

If [GDB] may act on it to display additional data in the future.

There is no XML for this feature as the presence of '`tpidr2`' is determined dynamically at runtime.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.1.6 AArch64 MTE registers feature

The '`org.gnu.gdb.aarch64.mte` could detect support for the Memory Tagging Extension and control memory tagging settings. If present, this feature must have the following register:

- \- '`tag_ctl`'.

Memory Tagging detection is done via a runtime check though, so the presence of this feature and register is not enough to enable memory tagging support.

This restriction may be lifted in the future.

Extra registers are allowed in this feature, but they will not affect [GDB].

---

::: header
Next: [ARC Features](ARC-Features.html#ARC-Features)]
:::
