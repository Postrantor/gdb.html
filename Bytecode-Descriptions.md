---
tip: translate by openai@2023-06-23 18:35:36
...
---
description: Bytecode Descriptions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Bytecode Descriptions (Debugging with GDB)
lang: en
resource-type: document
title: Bytecode Descriptions (Debugging with GDB)
---
::: header
Next: [Using Agent Expressions](Using-Agent-Expressions.html#Using-Agent-Expressions)]
:::

---

### F.2 Bytecode Descriptions


Each bytecode description has the following form:

> 每个字节码描述都具有以下形式：

`add` (0x02): `a`


:   Pop the top two stack items, `a`, as integers; push their sum, as an integer.

> 弹出栈顶的两个项目`a`，将它们作为整数；将它们的和作为一个整数压入栈中。


In this example, `add` is the name of the bytecode, and `(0x02)` is the one-byte value used to encode the bytecode, in hexadecimal. The phrase "`a`. There may be other values on the stack below those shown, but the bytecode affects only those shown.

> 在这个例子中，“add”是字节码的名称，“(0x02)”是用十六进制编码字节码的一个字节值。短语“a”。 堆栈中可能有其他值低于显示的值，但字节码仅影响显示的值。


Here is another example:

> 这是另一个例子：

`const8` (0x22) `n`


:   Push the 8-bit integer constant `n` on the stack, without sign extension.

> 将8位整数常量n压入堆栈，无需符号扩展。


In this example, the bytecode `const8` takes an operand `n` directly from the bytecode stream; the operand follows the `const8` bytecode itself. We write any such operands immediately after the name of the bytecode, before the colon, and describe the exact encoding of the operand in the bytecode stream in the body of the bytecode description.

> 在这个例子中，字节码`const8`从字节码流中直接获取操作数`n`；操作数会跟随`const8`字节码本身。我们在字节码名称后面的冒号之前写下任何这样的操作数，并在字节码描述的正文中描述操作数在字节码流中的确切编码。


For the `const8` bytecode, there are no stack items given before the ⇒; this simply means that the bytecode consumes no values from the stack. If a bytecode consumes no values, or produces no values, the list on either side of the ⇒ may be empty.

> 对于`const8`字节码，在⇒之前没有给出堆栈项；这意味着字节码不消耗堆栈中的任何值。如果字节码不消耗任何值或不产生任何值，则⇒两侧的列表可以为空。


If a value is written as `a`, then the bytecode treats it as an address.

> 如果一个值被写作`a`，那么字节码会将其视为一个地址。


We do not fully describe the floating point operations here; although this design can be extended in a clean way to handle floating point values, they are not of immediate interest to the customer, so we avoid describing them, to save time.

> 我们在这里没有完全描述浮点运算；尽管这个设计可以以一种干净的方式扩展以处理浮点值，但它们对客户来说不是当务之急，所以我们避免描述它们，以节省时间。

`float` (0x01): ⇒


:   Prefix for floating-point bytecodes. Not implemented yet.

> 前缀用于浮点字节码。尚未实施。

`add` (0x02): `a`


:   Pop two integers from the stack, and push their sum, as an integer.

> 从堆栈中弹出两个整数，并将它们的总和作为一个整数压入堆栈。

`sub` (0x03): `a`


:   Pop two integers from the stack, subtract the top value from the next-to-top value, and push the difference.

> 从堆栈中弹出两个整数，将顶部值减去次顶部值，并将差值压入堆栈。

`mul` (0x04): `a`


:   Pop two integers from the stack, multiply them, and push the product on the stack. Note that, when one multiplies two `n`-bit number, it is irrelevant whether the numbers are signed or not; the results are the same.

> 从堆栈中弹出两个整数，将它们相乘，然后将乘积推入堆栈。请注意，当乘以两个`n`位数时，它们是否有符号是无关紧要的；结果是相同的。

`div_signed` (0x05): `a`


:   Pop two signed integers from the stack; divide the next-to-top value by the top value, and push the quotient. If the divisor is zero, terminate with an error.

> 从堆栈中弹出两个带符号的整数；将次顶值除以顶值，并将商值压入堆栈。如果除数为零，则以错误终止。

`div_unsigned` (0x06): `a`


:   Pop two unsigned integers from the stack; divide the next-to-top value by the top value, and push the quotient. If the divisor is zero, terminate with an error.

> 从堆栈中弹出两个无符号整数；将次级值除以顶部值，并压入商数。如果除数为零，则以错误终止。

`rem_signed` (0x07): `a`


:   Pop two signed integers from the stack; divide the next-to-top value by the top value, and push the remainder. If the divisor is zero, terminate with an error.

> 从堆栈中弹出两个有符号整数；将次顶值除以顶值，并将余数压入堆栈。如果除数为零，则以错误终止。

`rem_unsigned` (0x08): `a`


:   Pop two unsigned integers from the stack; divide the next-to-top value by the top value, and push the remainder. If the divisor is zero, terminate with an error.

> 从堆栈弹出两个无符号整数；将次顶值除以顶值，并将余数压入堆栈。如果除数为零，则以错误终止。

`lsh` (0x09): `a`


:   Pop two integers from the stack; let `a` bits, and push the result.

> 从堆栈弹出两个整数；让`a`位，并把结果压入堆栈。

`rsh_signed` (0x0a): `a`


:   Pop two integers from the stack; let `a` bits, inserting copies of the top bit at the high end, and push the result.

> 从堆栈中弹出两个整数；让`a`位，在高端插入顶部位的副本，并将结果压入。

`rsh_unsigned` (0x0b): `a`


:   Pop two integers from the stack; let `a` bits, inserting zero bits at the high end, and push the result.

> 从堆栈中弹出两个整数；以a位长度，在高位插入零位，然后将结果压入堆栈。

`log_not` (0x0e): `a`


:   Pop an integer from the stack; if it is zero, push the value one; otherwise, push the value zero.

> 从堆栈中弹出一个整数；如果它是零，则推入值1；否则，推入值0。

`bit_and` (0x0f): `a`


:   Pop two integers from the stack, and push their bitwise `and`.

> 从堆栈弹出两个整数，并压入它们的按位与。

`bit_or` (0x10): `a`


:   Pop two integers from the stack, and push their bitwise `or`.

> 从堆栈中弹出两个整数，并压入它们的按位“或”。

`bit_xor` (0x11): `a`


:   Pop two integers from the stack, and push their bitwise exclusive-`or`.

> 从堆栈弹出两个整数，并将它们的按位排斥运算结果压入堆栈。

`bit_not` (0x12): `a`


:   Pop an integer from the stack, and push its bitwise complement.

> 从堆栈弹出一个整数，并压入其按位取反的值。

`equal` (0x13): `a`


:   Pop two integers from the stack; if they are equal, push the value one; otherwise, push the value zero.

> 从堆栈中弹出两个整数；如果它们相等，则压入值1；否则，压入值0。

`less_signed` (0x14): `a`


:   Pop two signed integers from the stack; if the next-to-top value is less than the top value, push the value one; otherwise, push the value zero.

> 从堆栈中弹出两个有符号整数；如果次顶值小于顶值，则将值推送为1；否则，将值推送为0。

`less_unsigned` (0x15): `a`


:   Pop two unsigned integers from the stack; if the next-to-top value is less than the top value, push the value one; otherwise, push the value zero.

> 从堆栈中弹出两个无符号整数；如果次顶值小于顶值，则将值推送到1；否则，将值推送到0。

`ext` (0x16) `n` bits


:   Pop an unsigned value from the stack; treating it as an `n` may be larger than or equal to the width of the stack elements of the bytecode engine; in this case, the bytecode should have no effect.

> 从堆栈弹出一个无符号值；将其视为可能大于或等于字节码引擎堆栈元素宽度的`n`；在这种情况下，字节码不应产生任何效果。

```
The number of source bits to preserve, `n`, is encoded as a single byte unsigned integer following the `ext` bytecode.
```

`zero_ext` (0x2a) `n` bits


:   Pop an unsigned value from the stack; zero all but the bottom `n` bits.

> 从堆栈弹出一个无符号值；将除底部n位以外的所有位都置零。

```
The number of source bits to preserve, `n`, is encoded as a single byte unsigned integer following the `zero_ext` bytecode.
```

`ref8` (0x17): `addr`
`ref16` (0x18): `addr`
`ref32` (0x19): `addr`
`ref64` (0x1a): `addr`


:   Pop an address `addr`, using the natural target endianness. Push the fetched value as an unsigned integer.

> 弹出一个地址`addr`，使用自然的目标端序。将获取的值作为无符号整数推送。

```
Note that `addr` may not be aligned in any particular way; the `refn` bytecodes should operate correctly for any address.

If attempting to access memory at `addr` would cause a processor exception of some sort, terminate with an error.
```

`ref_float` (0x1b): `addr`
`ref_double` (0x1c): `addr`
`ref_long_double` (0x1d): `addr`
`l_to_d` (0x1e): `a`
`d_to_l` (0x1f): `d`


:   Not implemented yet.

> 尚未实现。

`dup` (0x28): `a`


:   Push another copy of the stack's top element.

> 把堆栈顶部元素的另一个副本推入堆栈。

`swap` (0x2b): `a`


:   Exchange the top two items on the stack.

> 交换堆栈顶部的两个项目。

`pop` (0x29): `a` =\>


:   Discard the top value on the stack.

> 丢弃堆栈顶部的值。

`pick` (0x32) `n`


:   Duplicate an item from the stack and push it on the top of the stack. `n` exceeds the number of items on the stack, terminate with an error.

> 从堆栈中复制一个项目，并将其推到堆栈顶部。如果n超过堆栈中项目的数量，则报错终止。

`rot` (0x33): `a`


:   Rotate the top three items on the stack. The top item (c) becomes the third item, the next-to-top item (b) becomes the top item and the third item (a) from the top becomes the next-to-top item.

> 旋转堆栈顶部的三个项目。最顶部的项目（c）变成第三个项目，次顶部的项目（b）变成最顶部的项目，而最顶部的第三个项目（a）变成次顶部的项目。

`if_goto` (0x20) `offset` ⇒


:   Pop an integer off the stack; if it is non-zero, branch to the given offset in the bytecode string. Otherwise, continue to the next instruction in the bytecode stream. In other words, if `a`. Thus, an offset of zero denotes the beginning of the expression.

> 从堆栈中弹出一个整数; 如果它不为零，则跳转到字节码字符串中给定的偏移量。 否则，继续执行字节码流中的下一条指令。 换句话说，如果`a`。 因此，零偏移量表示表达式的开头。

```
The `offset` is stored as a sixteen-bit unsigned value, stored immediately following the `if_goto` bytecode. It is always stored most significant byte first, regardless of the target's normal endianness. The offset is not guaranteed to fall at any particular alignment within the bytecode stream; thus, on machines where fetching a 16-bit on an unaligned address raises an exception, you should fetch the offset one byte at a time.
```

`goto` (0x21) `offset`: ⇒


:   Branch unconditionally to `offset`.

> 无条件跳转到偏移量。

```
The offset is stored in the same way as for the `if_goto` bytecode.
```

`const8` (0x22) `n`
`const16` (0x23) `n`
`const32` (0x24) `n`
`const64` (0x25) `n`


:   Push the integer constant `n` on the stack, without sign extension. To produce a small negative value, push a small twos-complement value, and then sign-extend it using the `ext` bytecode.

> 将整数常量`n`压入堆栈，不带符号扩展。要产生一个小的负值，请使用`ext`字节码将小的二进制补码压入堆栈，然后进行符号扩展。

```
The constant `n` one byte at a time.
```

`reg` (0x26) `n`


:   Push the value of register number `n`, without sign extension. The registers are numbered following GDB's conventions.

> 将寄存器号码`n`的值推入，不扩展符号。寄存器按GDB的约定编号。

```
The register number `n` is encoded as a 16-bit unsigned integer immediately following the `reg` bytecode. It is always stored most significant byte first, regardless of the target's normal endianness. The register number is not guaranteed to fall at any particular alignment within the bytecode stream; thus, on machines where fetching a 16-bit on an unaligned address raises an exception, you should fetch the register number one byte at a time.
```

`getv` (0x2c) `n`


:   Push the value of trace state variable number `n`, without sign extension.

> 把跟踪状态变量编号`n`的值推送，不带符号扩展。

```
The variable number `n` is encoded as a 16-bit unsigned integer immediately following the `getv` bytecode. It is always stored most significant byte first, regardless of the target's normal endianness. The variable number is not guaranteed to fall at any particular alignment within the bytecode stream; thus, on machines where fetching a 16-bit on an unaligned address raises an exception, you should fetch the register number one byte at a time.
```

`setv` (0x2d) `n`


:   Set trace state variable number `n` is as described for `getv`.

> 设置跟踪状态变量编号`n`的描述与`getv`相同。

`trace` (0x0c): `addr` ⇒


:   Record the contents of the `size` in a trace buffer, for later retrieval by GDB.

> 记录`size`的内容到跟踪缓冲区，以便后续由GDB检索。

`trace_quick` (0x0d) `size`


:   Record the contents of the `size` is a single byte unsigned integer following the `trace` opcode.

> 记录`trace`操作码后面的`size`是一个单字节无符号整数。

```
This bytecode is equivalent to the sequence `dup const8 size trace`, but we provide it anyway to save space in bytecode strings.
```

`trace16` (0x30) `size`


:   Identical to trace_quick, except that `size` is a 16-bit big-endian unsigned integer, not a single byte. This should probably have been named `trace_quick16`, for consistency.

> 相比trace_quick，只有一个不同之处：`size`是一个16位的大端无符号整数，而不是单个字节。为了保持一致性，这里应该命名为`trace_quick16`。

`tracev` (0x2e) `n`


:   Record the value of trace state variable number `n` is as described for `getv`.

> 記錄追蹤狀態變量編號`n`的值如`getv`所述。

`tracenz` (0x2f) `addr` ⇒


:   Record the bytes at `addr` bytes have been recorded, whichever occurs first.

> 记录字节，从`addr`开始，直到先达到一个条件为止。

`printf` (0x34) `numargs` ⇒


:   Do a formatted print, in the style of the C function `printf`). The value of `numargs` stack elements, and pushes nothing.

> 请按照C函数`printf`的格式进行格式化打印，值为`numargs`堆栈元素，不推送任何内容。

`end` (0x27): ⇒


:   Stop executing bytecode; the result should be the top element of the stack. If the purpose of the expression was to compute an lvalue or a range of memory, then the next-to-top of the stack is the lvalue's address, and the top of the stack is the lvalue's size, in bytes.

> 停止执行字节码；结果应该是堆栈顶部的元素。如果表达式的目的是计算一个lvalue或一段内存，那么堆栈的次顶部是lvalue的地址，堆栈的顶部是lvalue的大小，以字节为单位。

---

::: header
Next: [Using Agent Expressions](Using-Agent-Expressions.html#Using-Agent-Expressions)]
:::
