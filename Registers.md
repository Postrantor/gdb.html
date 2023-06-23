---
description: Registers (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Registers (Debugging with GDB)
lang: en
resource-type: document
title: Registers (Debugging with GDB)
---
::: header
Next: [Floating Point Hardware](Floating-Point-Hardware.html#Floating-Point-Hardware)]
:::

---

### 10.14 Registers

You can refer to machine register contents, in expressions, as variables with names starting with '`$`'. The names of registers are different for each machine; use `info registers` to see the names used on your machine.

`info registers`

Print the names and values of all registers except floating-point and vector registers (in the selected stack frame).

`info all-registers`

Print the names and values of all registers, including floating-point and vector registers (in the selected stack frame).

`info registers reggroup …`

Print the name and value of the registers in each of the specified `reggroup` can be any of those returned by `maint print reggroups` (see [Maintenance Commands](Maintenance-Commands.html#Maintenance-Commands)).

`info registers regname …`

Print the *relativized* value of each specified register `regname`'.

[GDB] has four "standard" register names that are available (in expressions) on most machines---whenever they do not conflict with an architecture's canonical mnemonics for registers. The register names `$pc` and `$sp` are used for the program counter register and the stack pointer. `$fp` is used for a register that contains a pointer to the current stack frame, and `$ps` is used for a register that contains the processor status. For example, you could print the program counter in hex with

::: smallexample

```bash
p/x $pc
```

:::

or print the instruction to be executed next with

::: smallexample

```bash
x/i $pc
```

:::

or add four to the stack pointer[^12^](#FOOT12) with

::: smallexample

```bash
set $sp += 4
```

:::

Whenever possible, these four standard register names are available on your machine even though the machine has different canonical mnemonics, so long as there is no conflict. The `info registers` command shows the canonical names. For example, on the SPARC, `info registers` displays the processor status register as `$psr` but you can also refer to it as `$ps`; and on x86-based machines `$ps` is an alias for the [EFLAGS] register.

[GDB]').

Some registers have distinct "raw" and "virtual" data formats. This means that the data format in which the register contents are saved by the operating system is not the same one that your program normally sees. For example, the registers of the 68881 floating point coprocessor are always saved in "extended" (raw) format, but all C programs expect to work with "double" (virtual) format. In such cases, [GDB] normally works with the virtual format only (the format that makes sense for your program), but the `info registers` command prints the data in both formats.

Some machines have special registers whose contents can be interpreted in several different ways. For example, modern x86-based machines have SSE and MMX registers that can hold several values packed together in several different formats. [GDB] refers to such registers in `struct` notation:

::: smallexample

```bash
(gdb) print $xmm1
$1 = {
  v4_float = ,
  v2_double = ,
  v16_int8 = "\000\000\000\000\3706;\001\v\000\000\000\r\000\000",
  v8_int16 = ,
  v4_int32 = ,
  v2_int64 = ,
  uint128 = 0x0000000d0000000b013b36f800000000
}
```

:::

To set values of such registers, you need to tell [GDB] which view of the register you wish to change, as if you were assigning value to a `struct` member:

::: smallexample

```bash
 (gdb) set $xmm1.uint128 = 0x000000000000000000000000FFFFFFFF
```

:::

Normally, register values are relative to the selected stack frame (see [Selecting a Frame](Selection.html#Selection)). This means that you get the value that the register would contain if all stack frames farther in were exited and their saved registers restored. In order to see the true contents of hardware registers, you must select the innermost frame (with '`frame 0`').

Usually ABIs reserve some registers as not needed to be saved by the callee (a.k.a.: "caller-saved", "call-clobbered" or "volatile" registers). It may therefore not be possible for [GDB] has no knowledge of the register saving convention, if a register was not saved by the callee, then its value and location in the outer frame are assumed to be the same of the inner frame. This is usually harmless, because if the register is call-clobbered, the caller either does not care what is in the register after the call, or has code to restore the value that it does care about. Note, however, that if you change such a register in the outer frame, you may also be affecting the inner frame. Also, the more "outer" the frame is you're looking at, the more likely a call-clobbered register's value is to be wrong, in the sense that it doesn't actually represent the value the register had just before the call.

::: footnote

---

#### Footnotes

### [(12)](#DOCF12)

This is a way of removing one word from the stack, on machines where stacks grow downward in memory (most machines, nowadays). This assumes that the innermost stack frame is selected; setting `$sp` is not allowed when other stack frames are selected. To pop entire frames off the stack, regardless of machine architecture, use `return`; see [Returning from a Function](Returning.html#Returning).
:::

---

::: header
Next: [Floating Point Hardware](Floating-Point-Hardware.html#Floating-Point-Hardware)]
:::
