---
description: MIPS (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: MIPS (Debugging with GDB)
lang: en
resource-type: document
title: MIPS (Debugging with GDB)
---
::: header
Next: [HPPA](HPPA.html#HPPA)]
:::

---

#### 21.4.4 MIPS

Alpha- and MIPS-based computers use an unusual stack frame, which sometimes requires [GDB] to search backward in the object code to find the beginning of a function.

To improve response time (especially for embedded applications, where [GDB] may be restricted to a slow serial line for this search) you may want to limit the size of this search, using one of these commands:

`set heuristic-fence-post limit`

Restrict [GDB], the larger the limit the more bytes `heuristic-fence-post` must search and therefore the longer it takes to run. You should only need to use this command when debugging a stripped executable.

`show heuristic-fence-post`

Display the current limit.

These commands are available *only* when [GDB] is configured for debugging programs on Alpha or MIPS processors.

Several MIPS-specific commands are available when debugging MIPS programs:

`set mips abi arg`

Tell [GDB] are:

'`auto`'

The default ABI associated with the current binary (this is the default).

'`o32`'

'`o64`'

'`n32`'

'`n64`'

'`eabi32`'

'`eabi64`'

`show mips abi`

Show the MIPS ABI used by [GDB] to debug the inferior.

`set mips compression arg`

Tell [GDB] uses this for code disassembly and other internal interpretation purposes. This setting is only referred to when no executable has been associated with the debugging session or the executable does not provide information about the encoding it uses. Otherwise this setting is automatically updated from information provided by the executable.

Possible values of `arg`', as executables containing MIPS16 code frequently are not identified as such.

This setting is "sticky"; that is, it retains its value across debugging sessions until reset either explicitly with this command or implicitly from an executable.

The compiler and/or assembler typically add symbol table annotations to identify functions compiled for the MIPS16 or microMIPS ISAs. If these function-scope annotations are present, [GDB] uses them in preference to the global compressed ISA encoding setting.

`show mips compression`

Show the MIPS compressed ISA encoding used by [GDB] to debug the inferior.

`set mipsfpu`

`show mipsfpu`

See [set mipsfpu](MIPS-Embedded.html#MIPS-Embedded).

`set mips mask-address arg`

This command determines whether the most-significant 32 bits of 64-bit MIPS addresses are masked off. The argument `arg` determine the correct value.

`show mips mask-address`

Show whether the upper 32 bits of MIPS addresses are masked off or not.

`set remote-mips64-transfers-32bit-regs`

This command controls compatibility with 64-bit MIPS targets that transfer data in 32-bit quantities. If you have an old MIPS 64 target that transfers 32 bits for some registers, like [SR]'.

`show remote-mips64-transfers-32bit-regs`

Show the current setting of compatibility with older MIPS 64 targets.

`set debug mips`

This command turns on and off debugging messages for the MIPS-specific target code in [GDB].

`show debug mips`

Show the current setting of MIPS debugging messages.

---

::: header
Next: [HPPA](HPPA.html#HPPA)]
:::
