---
description: Machine Code (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Machine Code (Debugging with GDB)
lang: en
resource-type: document
title: Machine Code (Debugging with GDB)
---
::: header
Next: [Disable Reading Source](Disable-Reading-Source.html#Disable-Reading-Source)]
:::

---

### 9.6 Source and Machine Code

You can use the command `info line` to map source lines to program addresses (and vice versa), and the command `disassemble` to display a range of addresses as machine instructions. You can use the command `set disassemble-next-line` to set whether to disassemble next source line when execution stops. When run under [GNU] Emacs mode, the `info line` command causes the arrow to point to the line specified. Also, `info line` prints addresses in symbolic form as well as hex.

`info line`

`info line locspec`

Print the starting and ending addresses of the compiled code for the source lines of the code locations that result from resolving `locspec`, information about the current source line is printed.

For example, we can use `info line` to discover the location of the object code for the first line of function `m4_changequote`:

::: smallexample

```bash
(gdb) info line m4_changequote
Line 895 of "builtin.c" starts at pc 0x634c <m4_changequote> and \
        ends at 0x6350 <m4_changequote+4>.
```

:::

:

::: smallexample

```bash
(gdb) info line *0x63ff
Line 926 of "builtin.c" starts at pc 0x63e4 <m4_changequote+152> and \
        ends at 0x6404 <m4_changequote+184>.
```

:::

After `info line`, the default address for the `x` command is changed to the starting address of the line, so that '`x/i`' is sufficient to begin examining the machine code (see [Examining Memory](Memory.html#Memory)). Also, this address is saved as the value of the convenience variable `$_` (see [Convenience Variables](Convenience-Vars.html#Convenience-Vars)).

After `info line`, using `info line` again without specifying a location will display information about the next source line.

`disassemble`

`disassemble /m`

`disassemble /s`

`disassemble /r`

`disassemble /b`

This specialized command dumps a range of memory as machine instructions. It can also print mixed source+disassembly by specifying the `/m` or `/s` modifier and print the raw instructions in hex as well as in symbolic form by specifying the `/r` or `/b` modifier. The default memory range is the function surrounding the program counter of the selected frame. A single argument to this command is a program counter value; [GDB] dumps the function surrounding this value. When two arguments are given, they should be separated by a comma, possibly surrounded by whitespace. The arguments specify a range of addresses to dump, in one of two forms:

`start,end`

:   the addresses from `start` (exclusive)

`start,+length`

:   the addresses from `start` (inclusive) to `start+length` (exclusive).

When 2 arguments are specified, the name of the function is also printed (since there could be several functions in the given range).

The argument(s) can be any expression yielding a numeric value, such as '`0x32c4`'.

If the range of memory being disassembled contains current program counter, the instruction at that location is shown with a `=>` marker.

The following example shows the disassembly of a range of addresses of HP PA-RISC 2.0 code:

::: smallexample

```bash
(gdb) disas 0x32c4, 0x32e4
Dump of assembler code from 0x32c4 to 0x32e4:
   0x32c4 <main+204>:      addil 0,dp
   0x32c8 <main+208>:      ldw 0x22c(sr0,r1),r26
   0x32cc <main+212>:      ldil 0x3000,r31
   0x32d0 <main+216>:      ble 0x3f8(sr4,r31)
   0x32d4 <main+220>:      ldo 0(r31),rp
   0x32d8 <main+224>:      addil -0x800,dp
   0x32dc <main+228>:      ldo 0x588(r1),r26
   0x32e0 <main+232>:      ldil 0x3000,r31
End of assembler dump.
```

:::

The following two examples are for RISC-V, and demonstrates the difference between the `/r` and `/b` modifiers. First with `/b`, the bytes of the instruction are printed, in hex, in memory order:

::: smallexample

```bash
(gdb) disassemble /b 0x00010150,0x0001015c
Dump of assembler code from 0x10150 to 0x1015c:
   0x00010150 <call_me+4>:      22 dc                     sw  s0,56(sp)
   0x00010152 <call_me+6>:      80 00                     addi    s0,sp,64
   0x00010154 <call_me+8>:      23 26 a4 fe               sw  a0,-20(s0)
   0x00010158 <call_me+12>:     23 24 b4 fe               sw  a1,-24(s0)
End of assembler dump.
```

:::

In contrast, with `/r` the bytes of the instruction are displayed in the instruction order, for RISC-V this means that the bytes have been swapped to little-endian order:

::: smallexample

```bash
(gdb) disassemble /r 0x00010150,0x0001015c
Dump of assembler code from 0x10150 to 0x1015c:
   0x00010150 <call_me+4>:      dc22                  sw  s0,56(sp)
   0x00010152 <call_me+6>:      0080                  addi    s0,sp,64
   0x00010154 <call_me+8>:      fea42623          sw  a0,-20(s0)
   0x00010158 <call_me+12>:     feb42423          sw  a1,-24(s0)
End of assembler dump.
```

:::

Here is an example showing mixed source+assembly for Intel x86 with `/m` or `/s`, when the program is stopped just after function prologue in a non-optimized function with no inline code.

::: smallexample

```bash
(gdb) disas /m main
Dump of assembler code for function main:
5       {
   0x08048330 <+0>:    push   %ebp
   0x08048331 <+1>:    mov    %esp,%ebp
   0x08048333 <+3>:    sub    $0x8,%esp
   0x08048336 <+6>:    and    $0xfffffff0,%esp
   0x08048339 <+9>:    sub    $0x10,%esp

6         printf ("Hello.\n");
=> 0x0804833c <+12>:   movl   $0x8048440,(%esp)
   0x08048343 <+19>:   call   0x8048284 <puts@plt>

7         return 0;
8       }
   0x08048348 <+24>:   mov    $0x0,%eax
   0x0804834d <+29>:   leave
   0x0804834e <+30>:   ret

End of assembler dump.
```

:::

The `/m` option is deprecated as its output is not useful when there is either inlined code or re-ordered code. The `/s` option is the preferred choice. Here is an example for AMD x86-64 showing the difference between `/m` output and `/s` output. This example has one inline function defined in a header file, and the code is compiled with '`-O2`' optimization. Note how the `/m` output is missing the disassembly of several instructions that are present in the `/s` output.

`foo.h`:

::: smallexample

```bash
int
foo (int a)
{
  if (a < 0)
    return a * 2;
  if (a == 0)
    return 1;
  return a + 10;
}
```

:::

`foo.c`:

::: smallexample

```bash
#include "foo.h"
volatile int x, y;
int
main ()
{
  x = foo (y);
  return 0;
}
```

:::

::: smallexample

```bash
(gdb) disas /m main
Dump of assembler code for function main:
5   {

6     x = foo (y);
   0x0000000000400400 <+0>:   mov    0x200c2e(%rip),%eax # 0x601034 <y>
   0x0000000000400417 <+23>:  mov    %eax,0x200c13(%rip) # 0x601030 <x>

7     return 0;
8   }
   0x000000000040041d <+29>:  xor    %eax,%eax
   0x000000000040041f <+31>:  retq
   0x0000000000400420 <+32>:  add    %eax,%eax
   0x0000000000400422 <+34>:  jmp    0x400417 <main+23>

End of assembler dump.
(gdb) disas /s main
Dump of assembler code for function main:
foo.c:
5   {
6     x = foo (y);
   0x0000000000400400 <+0>:   mov    0x200c2e(%rip),%eax # 0x601034 <y>

foo.h:
4     if (a < 0)
   0x0000000000400406 <+6>:   test   %eax,%eax
   0x0000000000400408 <+8>:   js     0x400420 <main+32>

6     if (a == 0)
7       return 1;
8     return a + 10;
   0x000000000040040a <+10>:  lea    0xa(%rax),%edx
   0x000000000040040d <+13>:  test   %eax,%eax
   0x000000000040040f <+15>:  mov    $0x1,%eax
   0x0000000000400414 <+20>:  cmovne %edx,%eax

foo.c:
6     x = foo (y);
   0x0000000000400417 <+23>:  mov    %eax,0x200c13(%rip) # 0x601030 <x>

7     return 0;
8   }
   0x000000000040041d <+29>:  xor    %eax,%eax
   0x000000000040041f <+31>:  retq

foo.h:
5       return a * 2;
   0x0000000000400420 <+32>:  add    %eax,%eax
   0x0000000000400422 <+34>:  jmp    0x400417 <main+23>
End of assembler dump.
```

:::

Here is another example showing raw instructions in hex for AMD x86-64,

::: smallexample

```bash
(gdb) disas /r 0x400281,+10
Dump of assembler code from 0x400281 to 0x40028b:
   0x0000000000400281:  38 36  cmp    %dh,(%rsi)
   0x0000000000400283:  2d 36 34 2e 73 sub    $0x732e3436,%eax
   0x0000000000400288:  6f     outsl  %ds:(%rsi),(%dx)
   0x0000000000400289:  2e 32 00       xor    %cs:(%rax),%al
End of assembler dump.
```

:::

Note that the '`disassemble`'.

Some architectures have more than one commonly-used set of instruction mnemonics or other syntax.

For programs that were dynamically linked and use shared libraries, instructions that call functions or branch to locations in the shared libraries might show a seemingly bogus location---it's actually a location of the relocation table. On some architectures, [GDB] might be able to resolve these to actual function names.

`set disassembler-options option1[,option2…]`

This command controls the passing of target specific information to the disassembler. For a list of valid options, please refer to the `-M`/`--disassembler-options` section of the '`objdump` (see [objdump](http://sourceware.org/binutils/docs/binutils/objdump.html#objdump) in The GNU Binary Utilities). The default value is the empty string.

If it is necessary to specify more than one disassembler option, then multiple options can be placed together into a comma separated list. Currently this command is only supported on targets ARC, ARM, MIPS, PowerPC and S/390.

`show disassembler-options`

Show the current setting of the disassembler options.

`set disassembly-flavor instruction-set`

Select the instruction set to use when disassembling the program via the `disassemble` or `x/i` commands.

Currently this command is only defined for the Intel x86 family. You can set `instruction-set` to either `intel` or `att`. The default is `att`, the AT&T flavor used by default by Unix assemblers for x86-based targets.

`show disassembly-flavor`

Show the current setting of the disassembly flavor.

`set disassemble-next-line`

`show disassemble-next-line`

Control whether or not [GDB] to display some feedback when you step through a function with no line info or whose source file is unavailable. The default is OFF, which means never display the disassembly of the next line or instruction.

---

::: header
Next: [Disable Reading Source](Disable-Reading-Source.html#Disable-Reading-Source)]
:::
