---
description: General Bytecode Design (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: General Bytecode Design (Debugging with GDB)
lang: en
resource-type: document
title: General Bytecode Design (Debugging with GDB)
---
::: header
Next: [Bytecode Descriptions](Bytecode-Descriptions.html#Bytecode-Descriptions)]
:::

---

### F.1 General Bytecode Design

The agent represents bytecode expressions as an array of bytes. Each instruction is one byte long (thus the term *bytecode*). Some instructions are followed by operand bytes; for example, the `goto` instruction is followed by a destination for the jump.

The bytecode interpreter is a stack-based machine; most instructions pop their operands off the stack, perform some operation, and push the result back on the stack for the next instruction to consume. Each element of the stack may contain either a integer or a floating point value; these values are as many bits wide as the largest integer that can be directly manipulated in the source language. Stack elements carry no record of their type; bytecode could push a value as an integer, then pop it as a floating point value. However, GDB will not generate code which does this. In C, one might define the type of a stack element as follows:

::: example

```example
union agent_val {
  LONGEST l;
  DOUBLEST d;
};
```

:::

where `LONGEST` and `DOUBLEST` are `typedef` names for the largest integer and floating point types on the machine.

By the time the bytecode interpreter reaches the end of the expression, the value of the expression should be the only value left on the stack. For tracing applications, `trace` bytecodes in the expression will have recorded the necessary data, and the value on the stack may be discarded. For other applications, like conditional breakpoints, the value may be useful.

Separate from the stack, the interpreter has two registers:

`pc`

:   The address of the next bytecode to execute.

`start`

:   The address of the start of the bytecode expression, necessary for interpreting the `goto` and `if_goto` instructions.

Neither of these registers is directly visible to the bytecode language itself, but they are useful for defining the meanings of the bytecode operations.

There are no instructions to perform side effects on the running program, or call the program's functions; we assume that these expressions are only used for unobtrusive debugging, not for patching the running code.

Most bytecode instructions do not distinguish between the various sizes of values, and operate on full-width values; the upper bits of the values are simply ignored, since they do not usually make a difference to the value computed. The exceptions to this rule are:

memory reference instructions (`ref``n`)

:   There are distinct instructions to fetch different word sizes from memory. Once on the stack, however, the values are treated as full-size integers. They may need to be sign-extended; the `ext` instruction exists for this purpose.

the sign-extension instruction (`ext` `n`)

:   These clearly need to know which portion of their operand is to be extended to occupy the full length of the word.

If the interpreter is unable to evaluate an expression completely for some reason (a memory location is inaccessible, or a divisor is zero, for example), we say that interpretation "terminates with an error". This means that the problem is reported back to the interpreter's caller in some helpful way. In general, code using agent expressions should assume that they may attempt to divide by zero, fetch arbitrary memory locations, and misbehave in other ways.

Even complicated C expressions compile to a few bytecode instructions; for example, the expression `x + y * z` would typically produce code like the following, assuming that `x` and `y` live in registers, and `z` is a global variable holding a 32-bit `int`:

::: example

```example
reg 1
reg 2
const32 address of z
ref32
ext 32
mul
add
end
```

:::

In detail, these mean:

`reg 1`

:   Push the value of register 1 (presumably holding `x`) onto the stack.

`reg 2`

:   Push the value of register 2 (holding `y`).

`const32 address of z`

:   Push the address of `z` onto the stack.

`ref32`

:   Fetch a 32-bit word from the address at the top of the stack; replace the address on the stack with the value. Thus, we replace the address of `z` with `z`'s value.

`ext 32`

:   Sign-extend the value on the top of the stack from 32 bits to full length. This is necessary because `z` is a signed integer.

`mul`

:   Pop the top two numbers on the stack, multiply them, and push their product. Now the top of the stack contains the value of the expression `y * z`.

`add`

:   Pop the top two numbers, add them, and push the sum. Now the top of the stack contains the value of `x + y * z`.

`end`

:   Stop executing; the value left on the stack top is the value to be recorded.

---

::: header
Next: [Bytecode Descriptions](Bytecode-Descriptions.html#Bytecode-Descriptions)]
:::
