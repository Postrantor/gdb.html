---
tip: translate by openai@2023-06-23 17:33:25
...
---
description: ARM (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: ARM (Debugging with GDB)
lang: en
resource-type: document
title: ARM (Debugging with GDB)
---
::: header
Next: [BPF](BPF.html#BPF)]
:::

---

#### 21.3.2 ARM


[GDB] provides the following ARM-specific commands:

> [GDB] 提供以下专门针对ARM的命令：

`set arm disassembler`

:

```
This commands selects from a list of disassembly styles. The `"std"` style is the standard style.
```

`show arm disassembler`

:

```
Show the current disassembly style.
```

`set arm apcs32`

:

```
This command toggles ARM operation mode between 32-bit and 26-bit.
```

`show arm apcs32`


:   Display the current usage of the ARM 32-bit mode.

> 显示当前ARM 32位模式的使用情况。

`set arm fpu fputype`


:   This command sets the ARM floating-point unit (FPU) type. The argument `fputype` can be one of these:

> 此命令设置ARM浮点单元（FPU）类型。参数`fputype`可以是以下之一：

```
`auto`

:   Determine the FPU type by querying the OS ABI.

`softfpa`

:   Software FPU, with mixed-endian doubles on little-endian ARM processors.

`fpa`

:   GCC-compiled FPA co-processor.

`softvfp`

:   Software FPU with pure-endian doubles.

`vfp`

:   VFP co-processor.
```

`show arm fpu`


:   Show the current type of the FPU.

> 显示FPU的当前类型。

`set arm abi`


:   This command forces [GDB] to use the specified ABI.

> 这个命令强制[GDB]使用指定的ABI。

`show arm abi`


:   Show the currently used ABI.

> 显示当前使用的ABI。

`set arm fallback-mode (arm|thumb|auto)`


:   [GDB] to use the current execution mode (from the `T` bit in the `CPSR` register).

> 使用当前执行模式（来自CPSR寄存器中的T位）。

`show arm fallback-mode`


:   Show the current fallback instruction mode.

> 显示当前回退指令模式。

`set arm force-mode (arm|thumb|auto)`


:   This command overrides use of the symbol table to determine whether instructions are ARM or Thumb. The default is '`auto`'.

> 这个命令覆盖使用符号表来确定指令是ARM还是Thumb。默认是'自动'。

`show arm force-mode`


:   Show the current forced instruction mode.

> 显示当前强制指令模式。

`set arm unwind-secure-frames`


:   This command enables unwinding from Non-secure to Secure mode on Cortex-M with Security extension. This can trigger security exceptions when unwinding the exception stack. It is enabled by default.

> 这个命令可以使Cortex-M在具有安全扩展的情况下从非安全模式切换到安全模式。当异常堆栈撤销时，可能会触发安全异常。它默认情况下是启用的。

`show arm unwind-secure-frames`


:   Show whether unwinding from Non-secure to Secure mode is enabled.

> 检查从非安全模式到安全模式的解开是否已启用。

`set debug arm`


:   Toggle whether to display ARM-specific debugging messages from the ARM target support subsystem.

> 切换是否显示来自ARM目标支持子系统的ARM特定调试消息。

`show debug arm`


:   Show whether ARM-specific debugging messages are enabled.

> 检查ARM特定的调试消息是否已启用。

`target sim [simargs] …`


The [GDB] ARM simulator accepts the following optional arguments.

> GDB ARM 模拟器接受以下可选参数。

`--swi-support=type`


Tell the simulator which SWI interfaces to support. The argument `type` may be a comma separated list of the following values. The default value is `all`.

> 告诉模拟器支持哪些SWI接口。参数`type`可以是以下值的逗号分隔列表。默认值为`all`。

`none`

`demon`

`angel`

`redboot`

`all`

---

::: header
Next: [BPF](BPF.html#BPF)]
:::
