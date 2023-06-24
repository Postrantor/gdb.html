---
tip: translate by openai@2023-06-24 02:01:01
...
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

> 你可以在表达式中将机器寄存器内容引用为以'$'开头的变量。每台机器的寄存器名称不同；使用`info registers`查看你的机器上使用的名称。

`info registers`


Print the names and values of all registers except floating-point and vector registers (in the selected stack frame).

> 打印所选堆栈帧中所有非浮点和向量寄存器的名称和值。

`info all-registers`


Print the names and values of all registers, including floating-point and vector registers (in the selected stack frame).

> 打印所选堆栈帧中所有寄存器的名称和值，包括浮点和向量寄存器。

`info registers reggroup …`


Print the name and value of the registers in each of the specified `reggroup` can be any of those returned by `maint print reggroups` (see [Maintenance Commands](Maintenance-Commands.html#Maintenance-Commands)).

> 打印指定`reggroup`中每个寄存器的名称和值（可以参见[维护命令](Maintenance-Commands.html#Maintenance-Commands) 中 `maint print reggroups` 返回的任何一个）

`info registers regname …`

Print the *relativized* value of each specified register `regname`'.


[GDB] has four "standard" register names that are available (in expressions) on most machines---whenever they do not conflict with an architecture's canonical mnemonics for registers. The register names `$pc` and `$sp` are used for the program counter register and the stack pointer. `$fp` is used for a register that contains a pointer to the current stack frame, and `$ps` is used for a register that contains the processor status. For example, you could print the program counter in hex with

> [GDB]在大多数机器上提供了四个“标准”寄存器名称（在表达式中），只要它们不与体系结构的规范码冲突。寄存器名称`$pc`和`$sp`用于程序计数器寄存器和堆栈指针。`$fp`用于包含指向当前堆栈帧的指针的寄存器，`$ps`用于包含处理器状态的寄存器。例如，您可以使用十六进制打印程序计数器

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

> 只要没有冲突，就尽可能使用这四个标准寄存器名称，即使机器有不同的规范编码。`info registers`命令显示规范名称。例如，在SPARC上，`info registers`显示处理器状态寄存器为`$psr`，但您也可以将其称为`$ps`; 在基于x86的机器上，`$ps`是[EFLAGS]寄存器的别名。

[GDB]').


Some registers have distinct "raw" and "virtual" data formats. This means that the data format in which the register contents are saved by the operating system is not the same one that your program normally sees. For example, the registers of the 68881 floating point coprocessor are always saved in "extended" (raw) format, but all C programs expect to work with "double" (virtual) format. In such cases, [GDB] normally works with the virtual format only (the format that makes sense for your program), but the `info registers` command prints the data in both formats.

> 一些寄存器具有不同的“原始”和“虚拟”数据格式。这意味着操作系统保存寄存器内容的数据格式与您的程序通常看到的不同。例如，68881浮点数处理器的寄存器总是以“扩展”（原始）格式保存，但所有C程序都希望使用“双”（虚拟）格式工作。在这种情况下，[GDB]通常只使用虚拟格式（对您的程序有意义的格式），但`info registers`命令以两种格式打印数据。


Some machines have special registers whose contents can be interpreted in several different ways. For example, modern x86-based machines have SSE and MMX registers that can hold several values packed together in several different formats. [GDB] refers to such registers in `struct` notation:

> 一些机器具有特殊的寄存器，其内容可以以多种不同的方式解释。例如，现代基于x86的机器具有SSE和MMX寄存器，可以以多种不同的格式将多个值打包在一起。[GDB]在`struct`表示法中指的是这样的寄存器：

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

> 要设置这些寄存器的值，您需要告诉[GDB]您希望更改寄存器的视图，就像您将值分配给结构成员一样：

::: smallexample

```bash
 (gdb) set $xmm1.uint128 = 0x000000000000000000000000FFFFFFFF
```

:::


Normally, register values are relative to the selected stack frame (see [Selecting a Frame](Selection.html#Selection)). This means that you get the value that the register would contain if all stack frames farther in were exited and their saved registers restored. In order to see the true contents of hardware registers, you must select the innermost frame (with '`frame 0`').

> 一般来说，寄存器值是相对于所选择的堆栈帧（参见[选择帧](Selection.html#Selection)）的。这意味着，如果退出所有更深层的堆栈帧并恢复其保存的寄存器，你就可以获得该寄存器的值。要查看硬件寄存器的真实内容，必须选择最内层的帧（使用'`frame 0`'）。


Usually ABIs reserve some registers as not needed to be saved by the callee (a.k.a.: "caller-saved", "call-clobbered" or "volatile" registers). It may therefore not be possible for [GDB] has no knowledge of the register saving convention, if a register was not saved by the callee, then its value and location in the outer frame are assumed to be the same of the inner frame. This is usually harmless, because if the register is call-clobbered, the caller either does not care what is in the register after the call, or has code to restore the value that it does care about. Note, however, that if you change such a register in the outer frame, you may also be affecting the inner frame. Also, the more "outer" the frame is you're looking at, the more likely a call-clobbered register's value is to be wrong, in the sense that it doesn't actually represent the value the register had just before the call.

> 通常，ABI会将一些寄存器保留为被调用者（也称为“调用者保存”，“调用破坏”或“易失”寄存器）不需要保存的。因此，[GDB]可能不知道寄存器保存约定，如果寄存器未被调用者保存，则其值和外部帧中的位置假定与内部帧中的值相同。通常这是无害的，因为如果寄存器被调用破坏，调用者要么不在乎调用后寄存器中的值，要么有代码来恢复关心的值。但请注意，如果您在外部帧中更改此类寄存器，可能也会影响内部帧。此外，您正在查看的帧越“外部”，被调用破坏的寄存器的值越可能不正确，也就是说，它实际上不代表调用之前寄存器中的值。

::: footnote

---

#### Footnotes

### [(12)](#DOCF12)


This is a way of removing one word from the stack, on machines where stacks grow downward in memory (most machines, nowadays). This assumes that the innermost stack frame is selected; setting `$sp` is not allowed when other stack frames are selected. To pop entire frames off the stack, regardless of machine architecture, use `return`; see [Returning from a Function](Returning.html#Returning).

> 这是一种从堆栈中移除一个单词的方法，在内存中堆栈向下增长的机器上（现在大多数机器上）。这假定最内部的堆栈帧被选择；在选择其他堆栈帧时，不允许设置`$sp`。无论机器架构如何，要弹出整个帧，请使用`return`；请参见[从函数返回](Returning.html#Returning)。
:::

---

::: header
Next: [Floating Point Hardware](Floating-Point-Hardware.html#Floating-Point-Hardware)]
:::
