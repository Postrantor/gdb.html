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

`add` (0x02): `a`

:   Pop the top two stack items, `a`, as integers; push their sum, as an integer.

In this example, `add` is the name of the bytecode, and `(0x02)` is the one-byte value used to encode the bytecode, in hexadecimal. The phrase "`a`. There may be other values on the stack below those shown, but the bytecode affects only those shown.

Here is another example:

`const8` (0x22) `n`

:   Push the 8-bit integer constant `n` on the stack, without sign extension.

In this example, the bytecode `const8` takes an operand `n` directly from the bytecode stream; the operand follows the `const8` bytecode itself. We write any such operands immediately after the name of the bytecode, before the colon, and describe the exact encoding of the operand in the bytecode stream in the body of the bytecode description.

For the `const8` bytecode, there are no stack items given before the ⇒; this simply means that the bytecode consumes no values from the stack. If a bytecode consumes no values, or produces no values, the list on either side of the ⇒ may be empty.

If a value is written as `a`, then the bytecode treats it as an address.

We do not fully describe the floating point operations here; although this design can be extended in a clean way to handle floating point values, they are not of immediate interest to the customer, so we avoid describing them, to save time.

`float` (0x01): ⇒

:   Prefix for floating-point bytecodes. Not implemented yet.

`add` (0x02): `a`

:   Pop two integers from the stack, and push their sum, as an integer.

`sub` (0x03): `a`

:   Pop two integers from the stack, subtract the top value from the next-to-top value, and push the difference.

`mul` (0x04): `a`

:   Pop two integers from the stack, multiply them, and push the product on the stack. Note that, when one multiplies two `n`-bit number, it is irrelevant whether the numbers are signed or not; the results are the same.

`div_signed` (0x05): `a`

:   Pop two signed integers from the stack; divide the next-to-top value by the top value, and push the quotient. If the divisor is zero, terminate with an error.

`div_unsigned` (0x06): `a`

:   Pop two unsigned integers from the stack; divide the next-to-top value by the top value, and push the quotient. If the divisor is zero, terminate with an error.

`rem_signed` (0x07): `a`

:   Pop two signed integers from the stack; divide the next-to-top value by the top value, and push the remainder. If the divisor is zero, terminate with an error.

`rem_unsigned` (0x08): `a`

:   Pop two unsigned integers from the stack; divide the next-to-top value by the top value, and push the remainder. If the divisor is zero, terminate with an error.

`lsh` (0x09): `a`

:   Pop two integers from the stack; let `a` bits, and push the result.

`rsh_signed` (0x0a): `a`

:   Pop two integers from the stack; let `a` bits, inserting copies of the top bit at the high end, and push the result.

`rsh_unsigned` (0x0b): `a`

:   Pop two integers from the stack; let `a` bits, inserting zero bits at the high end, and push the result.

`log_not` (0x0e): `a`

:   Pop an integer from the stack; if it is zero, push the value one; otherwise, push the value zero.

`bit_and` (0x0f): `a`

:   Pop two integers from the stack, and push their bitwise `and`.

`bit_or` (0x10): `a`

:   Pop two integers from the stack, and push their bitwise `or`.

`bit_xor` (0x11): `a`

:   Pop two integers from the stack, and push their bitwise exclusive-`or`.

`bit_not` (0x12): `a`

:   Pop an integer from the stack, and push its bitwise complement.

`equal` (0x13): `a`

:   Pop two integers from the stack; if they are equal, push the value one; otherwise, push the value zero.

`less_signed` (0x14): `a`

:   Pop two signed integers from the stack; if the next-to-top value is less than the top value, push the value one; otherwise, push the value zero.

`less_unsigned` (0x15): `a`

:   Pop two unsigned integers from the stack; if the next-to-top value is less than the top value, push the value one; otherwise, push the value zero.

`ext` (0x16) `n` bits

:   Pop an unsigned value from the stack; treating it as an `n` may be larger than or equal to the width of the stack elements of the bytecode engine; in this case, the bytecode should have no effect.

```
The number of source bits to preserve, `n`, is encoded as a single byte unsigned integer following the `ext` bytecode.
```

`zero_ext` (0x2a) `n` bits

:   Pop an unsigned value from the stack; zero all but the bottom `n` bits.

```
The number of source bits to preserve, `n`, is encoded as a single byte unsigned integer following the `zero_ext` bytecode.
```

`ref8` (0x17): `addr`
`ref16` (0x18): `addr`
`ref32` (0x19): `addr`
`ref64` (0x1a): `addr`

:   Pop an address `addr`, using the natural target endianness. Push the fetched value as an unsigned integer.

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

`dup` (0x28): `a`

:   Push another copy of the stack's top element.

`swap` (0x2b): `a`

:   Exchange the top two items on the stack.

`pop` (0x29): `a` =\>

:   Discard the top value on the stack.

`pick` (0x32) `n`

:   Duplicate an item from the stack and push it on the top of the stack. `n` exceeds the number of items on the stack, terminate with an error.

`rot` (0x33): `a`

:   Rotate the top three items on the stack. The top item (c) becomes the third item, the next-to-top item (b) becomes the top item and the third item (a) from the top becomes the next-to-top item.

`if_goto` (0x20) `offset` ⇒

:   Pop an integer off the stack; if it is non-zero, branch to the given offset in the bytecode string. Otherwise, continue to the next instruction in the bytecode stream. In other words, if `a`. Thus, an offset of zero denotes the beginning of the expression.

```
The `offset` is stored as a sixteen-bit unsigned value, stored immediately following the `if_goto` bytecode. It is always stored most significant byte first, regardless of the target's normal endianness. The offset is not guaranteed to fall at any particular alignment within the bytecode stream; thus, on machines where fetching a 16-bit on an unaligned address raises an exception, you should fetch the offset one byte at a time.
```

`goto` (0x21) `offset`: ⇒

:   Branch unconditionally to `offset`.

```
The offset is stored in the same way as for the `if_goto` bytecode.
```

`const8` (0x22) `n`
`const16` (0x23) `n`
`const32` (0x24) `n`
`const64` (0x25) `n`

:   Push the integer constant `n` on the stack, without sign extension. To produce a small negative value, push a small twos-complement value, and then sign-extend it using the `ext` bytecode.

```
The constant `n` one byte at a time.
```

`reg` (0x26) `n`

:   Push the value of register number `n`, without sign extension. The registers are numbered following GDB's conventions.

```
The register number `n` is encoded as a 16-bit unsigned integer immediately following the `reg` bytecode. It is always stored most significant byte first, regardless of the target's normal endianness. The register number is not guaranteed to fall at any particular alignment within the bytecode stream; thus, on machines where fetching a 16-bit on an unaligned address raises an exception, you should fetch the register number one byte at a time.
```

`getv` (0x2c) `n`

:   Push the value of trace state variable number `n`, without sign extension.

```
The variable number `n` is encoded as a 16-bit unsigned integer immediately following the `getv` bytecode. It is always stored most significant byte first, regardless of the target's normal endianness. The variable number is not guaranteed to fall at any particular alignment within the bytecode stream; thus, on machines where fetching a 16-bit on an unaligned address raises an exception, you should fetch the register number one byte at a time.
```

`setv` (0x2d) `n`

:   Set trace state variable number `n` is as described for `getv`.

`trace` (0x0c): `addr` ⇒

:   Record the contents of the `size` in a trace buffer, for later retrieval by GDB.

`trace_quick` (0x0d) `size`

:   Record the contents of the `size` is a single byte unsigned integer following the `trace` opcode.

```
This bytecode is equivalent to the sequence `dup const8 size trace`, but we provide it anyway to save space in bytecode strings.
```

`trace16` (0x30) `size`

:   Identical to trace_quick, except that `size` is a 16-bit big-endian unsigned integer, not a single byte. This should probably have been named `trace_quick16`, for consistency.

`tracev` (0x2e) `n`

:   Record the value of trace state variable number `n` is as described for `getv`.

`tracenz` (0x2f) `addr` ⇒

:   Record the bytes at `addr` bytes have been recorded, whichever occurs first.

`printf` (0x34) `numargs` ⇒

:   Do a formatted print, in the style of the C function `printf`). The value of `numargs` stack elements, and pushes nothing.

`end` (0x27): ⇒

:   Stop executing bytecode; the result should be the top element of the stack. If the purpose of the expression was to compute an lvalue or a range of memory, then the next-to-top of the stack is the lvalue's address, and the top of the stack is the lvalue's size, in bytes.

---

::: header
Next: [Using Agent Expressions](Using-Agent-Expressions.html#Using-Agent-Expressions)]
:::
