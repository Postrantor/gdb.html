---
description: ARM Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: ARM Features (Debugging with GDB)
lang: en
resource-type: document
title: ARM Features (Debugging with GDB)
---
::: header
Next: [i386 Features](i386-Features.html#i386-Features)]
:::

---

#### G.5.3 ARM Features

#### G.5.3.1 Core register set for non-M-profile

The '`org.gnu.gdb.arm.core`' feature is required for non-M-profile ARM targets. It must contain the following registers:

- \- '`r0`'.
- \- '`sp`'.
- \- '`lr`', the link register. It is 32 bits in size.
- \- '`pc`'.
- \- '`cpsr`', the current program status register containing all the status bits. It is 32 bits in size. Historically this register was hardwired to number 25, but debugging stubs that report XML do not need to use this number anymore.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.3.2 Core register set for M-profile

For M-profile targets (e.g. Cortex-M3), the '`org.gnu.gdb.arm.core`', and it is a required feature. It must contain the following registers:

- \- '`r0`'.
- \- '`sp`'.
- \- '`lr`', the link register. It has a size of 32 bits.
- \- '`pc`'.
- \- '`xpsr`', the program status register containing all the status bits. It has a size of 32 bits. Historically this register was hardwired to number 25, but debugging stubs that report XML do not need to use this number anymore.

Upon seeing this feature, [GDB] will use hooks and configurations that are meaningful to M-profiles.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.3.3 FPA registers feature (obsolete)

The '`org.gnu.gdb.arm.fpa`' feature is obsolete and should not be advertised by debugging stubs anymore. It used to advertise registers for the old FPA architecture that has long been discontinued in toolchains.

It is kept in [GDB] for backward compatibility purposes so older debugging stubs that don't support XML target descriptions still work correctly. One such example is the KGDB debugging stub from Linux or BSD kernels.

The description below is for historical purposes only. This feature used to contain the following registers:

- \- '`f0`' is pinned to register number 16.
- \- '`fps`', the status register. It has a size of 32 bits.

#### G.5.3.4 M-profile Vector Extension (MVE)

Also known as Helium, the M-profile Vector Extension is advertised via the optional '`org.gnu.gdb.arm.m-profile-mve`' feature.

It must contain the following:

- \- '`vpr`' field from bits 20 to 23.

  Bits 24 through 31 are reserved.

When this feature is available, [GDB]' contents.

This feature must only be advertised if the target is M-profile. Advertising this feature for targets that are not M-profile may cause [GDB] to assume the target is M-profile when it isn't.

If the '`org.gnu.gdb.arm.vfp`' register contents.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.3.5 XScale iwMMXt feature

The XScale '`org.gnu.gdb.xscale.iwmmxt`' feature is optional. If present, it must contain the following:

- \- '`wR0`'.
- \- '`wCGR0`'.

The following registers are optional:

- \- '`wCID`'.
- \- '`wCon`'.
- \- '`wCSSF`'.
- \- '`wCASF`'.

This feature should only be reported if the target is XScale.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.3.6 Vector Floating-Point (VFP) feature

The '`org.gnu.gdb.arm.vfp`' feature is optional. If present, it should contain one of two possible sets of values depending on whether VFP version 2 or VFP version 3 is in use.

For VFP v2:

- \- '`d0`'.
- \- '`fpscr`'.

For VFP v3:

- \- '`d0`'.
- \- '`fpscr`'.

If this feature is available, [GDB] will synthesize the single-precision floating-point registers from halves of the double-precision registers as pseudo-registers.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.3.7 NEON architecture feature

The '`org.gnu.gdb.arm.neon`' must also be present and include 32 double-precision registers.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.3.8 M-profile Pointer Authentication and Branch Target Identification feature

The '`org.gnu.gdb.arm.m-profile-pacbti`' feature is optional, and acknowledges support for the ARMv8.1-m PACBTI extensions.

This feature doesn't contain any required registers, and it only serves as a hint to [GDB] that the debugging stub supports the ARMv8.1-m PACBTI extensions.

When [GDB] sees this feature, it will track return address signing states and will decorate backtraces using the \[PAC] marker, similar to AArch64's PAC extension. See [AArch64 PAC](AArch64.html#AArch64-PAC).

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.3.9 M-profile system registers feature

The '`org.gnu.gdb.arm.m-system` about additional system registers.

At the moment this feature must contain the following:

- \- '`msp`'.
- \- '`psp`'.

This feature must only be advertised for M-profile targets. When [GDB]' across frames.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.3.10 M-profile Security Extensions feature

The '`org.gnu.gdb.arm.secext` could better support the switching of stack pointers and secure states in the Security Extensions.

At the moment this feature must contain the following:

- \- '`msp_ns`'.
- \- '`psp_ns`'.
- \- '`msp_s`'.
- \- '`psp_s`'.

When [GDB] sees this feature, it will attempt to track the values of all 4 stack pointers across secure state transitions, potentially improving unwinding when applications switch between security states.

Extra registers are allowed in this feature, but they will not affect [GDB].

#### G.5.3.11 TLS registers feature

The optional '`org.gnu.gdb.arm.tls`' feature contains TLS registers.

Currently it contains the following:

- \- '`tpidruro`'.

At the moment [GDB] looks for this feature, but doesn't do anything with it other than displaying it.

Extra registers are allowed in this feature, but they will not affect [GDB].

---

::: header
Next: [i386 Features](i386-Features.html#i386-Features)]
:::
