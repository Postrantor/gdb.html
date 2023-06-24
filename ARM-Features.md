---
tip: translate by openai@2023-06-23 17:29:28
...
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

> `org.gnu.gdb.arm.core`功能对于非M-profile ARM目标是必需的，它必须包含以下寄存器：

- \- '`r0`'.
- \- '`sp`'.
- \- '`lr`', the link register. It is 32 bits in size.
- \- '`pc`'.

- \- '`cpsr`', the current program status register containing all the status bits. It is 32 bits in size. Historically this register was hardwired to number 25, but debugging stubs that report XML do not need to use this number anymore.

> 当前程序状态寄存器(CPSR)包含所有状态位，其大小为32位。历史上，该寄存器的编号固定为25，但不再需要使用这个编号的调试存根可以报告XML。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中被允许，但它们不会影响[GDB]。

#### G.5.3.2 Core register set for M-profile


For M-profile targets (e.g. Cortex-M3), the '`org.gnu.gdb.arm.core`', and it is a required feature. It must contain the following registers:

> 对于M-profile目标（例如Cortex-M3），必须包含以下寄存器的“org.gnu.gdb.arm.core”功能。

- \- '`r0`'.
- \- '`sp`'.
- \- '`lr`', the link register. It has a size of 32 bits.
- \- '`pc`'.

- \- '`xpsr`', the program status register containing all the status bits. It has a size of 32 bits. Historically this register was hardwired to number 25, but debugging stubs that report XML do not need to use this number anymore.

> XPSR程序状态寄存器包含所有状态位，其位数为32位。从历史上看，该寄存器的硬编码编号为25，但报告XML的调试存根不再需要使用此编号。


Upon seeing this feature, [GDB] will use hooks and configurations that are meaningful to M-profiles.

> 看到这个特性时，GDB将使用对M-profiles有意义的钩子和配置。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中是允许的，但它们不会影响GDB。

#### G.5.3.3 FPA registers feature (obsolete)


The '`org.gnu.gdb.arm.fpa`' feature is obsolete and should not be advertised by debugging stubs anymore. It used to advertise registers for the old FPA architecture that has long been discontinued in toolchains.

> 'org.gnu.gdb.arm.fpa' 特性已经过时，调试存根不应再宣传它。它曾经宣传早已在工具链中被废弃的旧FPA架构的寄存器。


It is kept in [GDB] for backward compatibility purposes so older debugging stubs that don't support XML target descriptions still work correctly. One such example is the KGDB debugging stub from Linux or BSD kernels.

> 它被保存在GDB中，以便支持向后兼容，因此不支持XML目标描述的旧调试存根仍然可以正确工作。其中一个例子是来自Linux或BSD内核的KGDB调试存根。


The description below is for historical purposes only. This feature used to contain the following registers:

> 以下描述仅供参考历史用途。此功能曾包含以下寄存器：

- \- '`f0`' is pinned to register number 16.
- \- '`fps`', the status register. It has a size of 32 bits.

#### G.5.3.4 M-profile Vector Extension (MVE)


Also known as Helium, the M-profile Vector Extension is advertised via the optional '`org.gnu.gdb.arm.m-profile-mve`' feature.

> 也被称为氦，M-profile Vector Extension可以通过可选的'org.gnu.gdb.arm.m-profile-mve'功能来宣传。


It must contain the following:

> 它必须包含以下内容:

- \- '`vpr`' field from bits 20 to 23.


  Bits 24 through 31 are reserved.

> 位24至31保留。


When this feature is available, [GDB]' contents.

> 当这个功能可用时，[GDB]的内容。


This feature must only be advertised if the target is M-profile. Advertising this feature for targets that are not M-profile may cause [GDB] to assume the target is M-profile when it isn't.

> 这个特性只有在目标是M-profile时才能宣传。对于不是M-profile的目标宣传这个特性可能会导致[GDB]误以为目标是M-profile，其实并不是。


If the '`org.gnu.gdb.arm.vfp`' register contents.

> 如果有“org.gnu.gdb.arm.vfp”寄存器的内容。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中允许使用，但它们不会影响GDB。

#### G.5.3.5 XScale iwMMXt feature


The XScale '`org.gnu.gdb.xscale.iwmmxt`' feature is optional. If present, it must contain the following:

> XScale' 'org.gnu.gdb.xscale.iwmmxt'功能是可选的。如果存在，它必须包含以下内容：

- \- '`wR0`'.
- \- '`wCGR0`'.


The following registers are optional:

> 以下注册是可选的：

- \- '`wCID`'.
- \- '`wCon`'.
- \- '`wCSSF`'.
- \- '`wCASF`'.


This feature should only be reported if the target is XScale.

> 这个功能只有在目标是XScale时才应该报告。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在这个特性中是允许的，但它们不会影响[GDB]。

#### G.5.3.6 Vector Floating-Point (VFP) feature


The '`org.gnu.gdb.arm.vfp`' feature is optional. If present, it should contain one of two possible sets of values depending on whether VFP version 2 or VFP version 3 is in use.

> 该'org.gnu.gdb.arm.vfp'功能是可选的。如果存在，它应该包含两种可能的值集之一，取决于是使用VFP版本2还是VFP版本3。

For VFP v2:

- \- '`d0`'.
- \- '`fpscr`'.

For VFP v3:

- \- '`d0`'.
- \- '`fpscr`'.


If this feature is available, [GDB] will synthesize the single-precision floating-point registers from halves of the double-precision registers as pseudo-registers.

> 如果此功能可用，[GDB]将从双精度寄存器的一半合成单精度浮点寄存器，作为伪寄存器。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中是允许的，但是它们不会影响GDB。

#### G.5.3.7 NEON architecture feature


The '`org.gnu.gdb.arm.neon`' must also be present and include 32 double-precision registers.

> 'org.gnu.gdb.arm.neon'必须存在并包含32个双精度寄存器。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中是允许的，但它们不会影响GDB。

#### G.5.3.8 M-profile Pointer Authentication and Branch Target Identification feature


The '`org.gnu.gdb.arm.m-profile-pacbti`' feature is optional, and acknowledges support for the ARMv8.1-m PACBTI extensions.

> 这个'org.gnu.gdb.arm.m-profile-pacbti'功能是可选的，它承认对ARMv8.1-m PACBTI扩展的支持。


This feature doesn't contain any required registers, and it only serves as a hint to [GDB] that the debugging stub supports the ARMv8.1-m PACBTI extensions.

> 此功能不包含任何必需的寄存器，仅提供暗示给GDB，该调试存根支持ARMv8.1-m PACBTI扩展。


When [GDB] sees this feature, it will track return address signing states and will decorate backtraces using the \[PAC] marker, similar to AArch64's PAC extension. See [AArch64 PAC](AArch64.html#AArch64-PAC).

> 当GDB看到这个功能时，它将跟踪返回地址签名状态，并使用PAC标记装饰回溯，类似于AArch64的PAC扩展。参见AArch64 PAC（AArch64.html#AArch64-PAC）。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中是允许的，但它们不会影响[GDB]。

#### G.5.3.9 M-profile system registers feature


The '`org.gnu.gdb.arm.m-system` about additional system registers.

> 这个"org.gnu.gdb.arm.m-system"涉及到额外的系统寄存器。


At the moment this feature must contain the following:

> 此时此刻，此功能必须包含以下内容：

- \- '`msp`'.
- \- '`psp`'.


This feature must only be advertised for M-profile targets. When [GDB]' across frames.

> 这个功能只能针对M型目标进行广告宣传。当[GDB]跨越框架时。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在这个功能中是允许的，但它们不会影响[GDB]。

#### G.5.3.10 M-profile Security Extensions feature


The '`org.gnu.gdb.arm.secext` could better support the switching of stack pointers and secure states in the Security Extensions.

> 'org.gnu.gdb.arm.secext'可以更好地支持安全扩展中的堆栈指针和安全状态的切换。


At the moment this feature must contain the following:

> 此时此刻，此功能必须包含以下内容：

- \- '`msp_ns`'.
- \- '`psp_ns`'.
- \- '`msp_s`'.
- \- '`psp_s`'.


When [GDB] sees this feature, it will attempt to track the values of all 4 stack pointers across secure state transitions, potentially improving unwinding when applications switch between security states.

> 当GDB看到这个特性时，它将尝试跟踪所有4个堆栈指针在安全状态转换期间的值，可能会改善当应用程序在安全状态之间切换时的解开过程。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中可以使用，但是它们不会影响[GDB]。

#### G.5.3.11 TLS registers feature


The optional '`org.gnu.gdb.arm.tls`' feature contains TLS registers.

> 可选的'org.gnu.gdb.arm.tls'功能包含TLS寄存器。


Currently it contains the following:

> 目前它包含以下内容：

- \- '`tpidruro`'.


At the moment [GDB] looks for this feature, but doesn't do anything with it other than displaying it.

> 目前，[GDB]正在寻找这个功能，但除了显示它之外，没有做任何其他事情。


Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在这个功能中是允许的，但它们不会影响[GDB]。

---

::: header
Next: [i386 Features](i386-Features.html#i386-Features)]
:::
