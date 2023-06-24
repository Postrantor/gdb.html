---
tip: translate by openai@2023-06-23 16:46:27
...
---
description: AArch64 Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: AArch64 Features (Debugging with GDB)
lang: en
resource-type: document
title: AArch64 Features (Debugging with GDB)
--------------------------------------------

::: header
Next: [ARC Features](ARC-Features.html#ARC-Features)]
:::

---

#### G.5.1 AArch64 Features

#### G.5.1.1 AArch64 core registers feature

The '`org.gnu.gdb.aarch64.core`' feature is required for AArch64 targets. It must contain the following:

> 要使用 AArch64 目标，必须拥有'org.gnu.gdb.aarch64.core'功能。它必须包含以下内容：

- \- '`x0`'.
- \- '`sp`'.
- \- '`pc`'.
- \- '`cpsr`', the current program status register. It is 32 bits in size and has a custom flags type.

> 当前程序状态寄存器 CPSR，其大小为 32 位，具有自定义标志类型。

The semantics of the individual flags and fields in '`cpsr`' can change as new architectural features are added. The current layout can be found in the aarch64-core.xml file.

> 'cpsr'中各个标志和字段的语义会随着新的架构特性的添加而发生变化。当前的布局可以在 aarch64-core.xml 文件中找到。

Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中是允许的，但它们不会影响[GDB]。

#### G.5.1.2 AArch64 floating-point registers feature

The '`org.gnu.gdb.aarch64.fpu`' feature is optional. If present, it must contain the following registers:

> 'org.gnu.gdb.aarch64.fpu'功能是可选的。如果存在，它必须包含以下寄存器：

- \- '`v0`', the vector registers with size of 128 bits. The type is a custom vector type.
- \- '`fpsr`', the floating-point status register. It is 32 bits in size and has a custom flags type.

> 浮点状态寄存器(FPSR)，其大小为 32 位，有自定义标志类型。

- \- '`fpcr`', the floating-point control register. It is 32 bits in size and has a custom flags type.

> 浮点控制寄存器（FPCR），32 位，具有自定义标志类型。

The semantics of the individual flags and fields in '`fpsr`' can change as new architectural features are added.

> 'fpsr'中各个标志和字段的语义会随着新的架构特性的增加而发生变化。

The types for the vector registers, '`fpsr`' registers can be found in the aarch64-fpu.xml file.

> 可以在 aarch64-fpu.xml 文件中找到向量寄存器 `fpsr` 寄存器的类型。

Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在这个功能中是允许的，但它们不会影响 GDB。

#### G.5.1.3 AArch64 SVE registers feature

The '`org.gnu.gdb.aarch64.sve`' feature is optional. If present, it means the target supports the Scalable Vector Extension and must contain the following registers:

> org.gnu.gdb.aarch64.sve 功能是可选的。如果存在，则表示目标支持可伸缩矢量扩展，并且必须包含以下寄存器：

- \- '`z0`', the scalable vector registers. Their sizes are variable and a multiple of 128 bits up to a maximum of 2048 bit. Their type is a custom union type that helps visualize different sizes of sub-vectors.

> - \- '`z0`'，可伸缩的矢量寄存器。它们的大小是可变的，最大可达 2048 位，每次增加 128 位。它们的类型是一种自定义的联合类型，有助于可视化不同大小的子矢量。

- \- '`fpsr`', the floating-point status register. It is 32 bits in size and has a custom flags type.

> 浮点状态寄存器（FPSR），32 位大小，具有自定义标志类型。

- \- '`fpcr`', the floating-point control register. It is 32 bits in size and has a custom flags type.

> 浮点控制寄存器(FPCR)，32 位大小，具有自定义标志类型。

- \- '`p0`', the predicate registers. Their sizes are variable, based on the current vector length, and a multiple of 16 bits. Their types are a custom union to help visualize sub-elements.

> - \- '`p0`'，谓词寄存器的大小是可变的，根据当前向量长度和 16 位的倍数而定。它们的类型是一个自定义的联合体，可以帮助可视化子元素。

- \- '`ffr`', the First Fault register. It has a variable size based on the current vector length and is a multiple of 16 bits. The type is the same as the predicate registers.

> 第一故障寄存器（FFR），其大小取决于当前向量长度，且是 16 位的整数倍。类型与谓词寄存器相同。

- \- '`vg`'.

When [GDB]'.

[GDB]' feature.

The first 128 bits of the '`z`' registers, so changing one will trigger a change to the other.

> 第一个 `z` 寄存器的前 128 位，因此改变其中一个将触发对另一个的改变。

For the types of the '`z`' registers, please check the aarch64-sve.c file. No XML file is available for this feature because it is dynamically generated based on the current vector length.

> 对于'z'寄存器的类型，请查看 aarch64-sve.c 文件。没有 XML 文件可用于此功能，因为它是基于当前向量长度动态生成的。

The semantics of the individual flags and fields in '`fpsr`' can change as new architectural features are added.

> `fpsr` 中的各个标志和字段的语义可以随着新的架构特性的添加而改变。

The types for the '`fpsr`' registers can be found in the aarch64-sve.c file, and should match what is described in aarch64-fpu.xml.

> 在 aarch64-sve.c 文件中可以找到'fpsr'寄存器的类型，并且应该与 aarch64-fpu.xml 中描述的相匹配。

Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中是允许的，但它们不会影响 GDB。

#### G.5.1.4 AArch64 Pointer Authentication registers feature

The '`org.gnu.gdb.aarch64.pauth` could detect support for the Pointer Authentication extension. If present, it must contain one of two possible register sets.

> `org.gnu.gdb.aarch64.pauth` 可以检测指针认证扩展的支持情况。如果存在，它必须包含两个可能的寄存器集之一。

Pointer Authentication masks for user-mode:

> 指针认证掩码用于用户模式

- \- '`pauth_dmask`', the user-mode pointer authentication mask for data pointers. It is 64 bits in size.

> 用户模式指针认证掩码 `pauth_dmask`，用于数据指针，大小为 64 位。

- \- '`pauth_cmask`', the user-mode pointer authentication mask for code pointers. It is 64 bits in size.

> `-\- 'pauth_cmask`'，代码指针的用户模式指针验证掩码，大小为 64 位。

Pointer Authentication masks for user-mode and kernel-mode:

> 指针认证掩码用于用户模式和内核模式：

- \- '`pauth_dmask`', the user-mode pointer authentication mask for data pointers. It is 64 bits in size.

> 用户模式指针认证掩码（`pauth_dmask`），用于数据指针，大小为 64 位。

- \- '`pauth_cmask`', the user-mode pointer authentication mask for code pointers. It is 64 bits in size.

> `-\-` pauth_cmask` 是用户模式指针认证掩码，用于代码指针，大小为 64 位。

- \- '`pauth_dmask_high`', the kernel-mode pointer authentication mask for data pointers. It is 64 bits in size.

> `-\-'是内核模式指针认证掩码（pauth_dmask_high），用于数据指针，大小为 64 位。

- \- '`pauth_cmask_high`', the kernel-mode pointer authentication mask for code pointers. It is 64 bits in size.

> `- \- '` pauth_cmask_high`'，内核模式代码指针验证掩码，长度为 64 位。

If [GDB]' marker alongside a function that has a signed link register value that needs to be unmasked/decoded.

> 如果[GDB]标记放在一个有着需要解除掩码/解码的有符号链接寄存器值的函数旁边。

[GDB] will also use the masks to remove non-address bits from pointers.

> GDB 也会使用掩码来从指针中移除非地址位。

Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中是允许的，但它们不会影响[GDB]。

Please note the '`org.gnu.gdb.aarch64.pauth`' feature string instead.

> 请注意'org.gnu.gdb.aarch64.pauth'特性字符串。

The '`org.gnu.gdb.aarch64.pauth_v2`'.

> org.gnu.gdb.aarch64.pauth_v2 的简体中文

The reason for having feature '`org.gnu.gdb.aarch64.pauth_v2`. This is more common when using emulators and on bare-metal debugging scenarios.

> 这个特性'org.gnu.gdb.aarch64.pauth_v2'的原因。这在使用模拟器和裸机调试场景中更为常见。

It can also happen if a newer gdbserver is used with an old [GDB] does not know about, potentially leading to a crash.

> 这也可能发生在一个较新的 gdbserver 被用于一个[GDB]不知道的旧版本时，可能导致崩溃。

#### G.5.1.5 AArch64 TLS registers feature

The '`org.gnu.gdb.aarch64.tls`. If present, it must contain either one of the following register sets.

> 如果存在，它必须包含以下注册集中的一个：'org.gnu.gdb.aarch64.tls'。

Only '`tpidr`':

- \- '`tpidr`'.

Both '`tpidr`'.

- \- '`tpidr`'.
- \- '`tpidr2`'. It may be used in the future alongside the Scalable Matrix Extension for a lazy restore scheme.

> - \- '`TPIDR2`'将与可扩展矩阵扩展一起用于懒惰恢复方案，将来可能会使用。

If [GDB] may act on it to display additional data in the future.

> 如果 GDB 可以在将来对它采取行动以显示额外的数据。

There is no XML for this feature as the presence of '`tpidr2`' is determined dynamically at runtime.

> 没有 XML 可以用来支持这个特性，因为'`tpidr2`'的存在是在运行时动态确定的。

Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在这个功能中是允许的，但是它们不会影响[GDB]。

#### G.5.1.6 AArch64 MTE registers feature

The '`org.gnu.gdb.aarch64.mte` could detect support for the Memory Tagging Extension and control memory tagging settings. If present, this feature must have the following register:

> `org.gnu.gdb.aarch64.mte` 可以检测对内存标记扩展的支持情况，并控制内存标记设置。如果存在，此功能必须具有以下寄存器：

- \- '`tag_ctl`'.

Memory Tagging detection is done via a runtime check though, so the presence of this feature and register is not enough to enable memory tagging support.

> 内存标记检测是通过运行时检查完成的，因此仅仅存在这个功能和寄存器是不足以启用内存标记支持的。

This restriction may be lifted in the future.

> 未来可能会解除此限制。

Extra registers are allowed in this feature, but they will not affect [GDB].

> 额外的寄存器在此功能中是允许的，但它们不会影响 GDB。

---

::: header
Next: [ARC Features](ARC-Features.html#ARC-Features)]
:::
