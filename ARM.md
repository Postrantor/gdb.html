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

`set arm fpu fputype`

:   This command sets the ARM floating-point unit (FPU) type. The argument `fputype` can be one of these:

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

`set arm abi`

:   This command forces [GDB] to use the specified ABI.

`show arm abi`

:   Show the currently used ABI.

`set arm fallback-mode (arm|thumb|auto)`

:   [GDB] to use the current execution mode (from the `T` bit in the `CPSR` register).

`show arm fallback-mode`

:   Show the current fallback instruction mode.

`set arm force-mode (arm|thumb|auto)`

:   This command overrides use of the symbol table to determine whether instructions are ARM or Thumb. The default is '`auto`'.

`show arm force-mode`

:   Show the current forced instruction mode.

`set arm unwind-secure-frames`

:   This command enables unwinding from Non-secure to Secure mode on Cortex-M with Security extension. This can trigger security exceptions when unwinding the exception stack. It is enabled by default.

`show arm unwind-secure-frames`

:   Show whether unwinding from Non-secure to Secure mode is enabled.

`set debug arm`

:   Toggle whether to display ARM-specific debugging messages from the ARM target support subsystem.

`show debug arm`

:   Show whether ARM-specific debugging messages are enabled.

`target sim [simargs] …`

The [GDB] ARM simulator accepts the following optional arguments.

`--swi-support=type`

Tell the simulator which SWI interfaces to support. The argument `type` may be a comma separated list of the following values. The default value is `all`.

`none`

`demon`

`angel`

`redboot`

`all`

---

::: header
Next: [BPF](BPF.html#BPF)]
:::
