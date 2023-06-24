---
tip: translate by openai@2023-06-23 22:38:58
...
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

> 代理人将字节码表达式表示为字节数组。每条指令长度为一个字节（因此称为*字节码*）。一些指令后跟操作数字节；例如，`goto`指令后跟跳转的目的地。


The bytecode interpreter is a stack-based machine; most instructions pop their operands off the stack, perform some operation, and push the result back on the stack for the next instruction to consume. Each element of the stack may contain either a integer or a floating point value; these values are as many bits wide as the largest integer that can be directly manipulated in the source language. Stack elements carry no record of their type; bytecode could push a value as an integer, then pop it as a floating point value. However, GDB will not generate code which does this. In C, one might define the type of a stack element as follows:

> 字节码解释器是一种基于堆栈的机器；大多数指令从堆栈中弹出其操作数，执行某些操作，并将结果推回堆栈，供下一条指令使用。堆栈的每个元素可以包含整数或浮点值；这些值的位数与源语言中可直接操作的最大整数的位数相同。堆栈元素不记录其类型；字节码可以将值作为整数推入，然后将其作为浮点值弹出。但是，GDB不会生成这样的代码。在C中，可以如下定义堆栈元素的类型：

::: example

```example
union agent_val {
  LONGEST l;
  DOUBLEST d;
};
```

:::


where `LONGEST` and `DOUBLEST` are `typedef` names for the largest integer and floating point types on the machine.

> 在机器上，`LONGEST` 和 `DOUBLEST` 是最大整数和浮点类型的`typedef`名称。


By the time the bytecode interpreter reaches the end of the expression, the value of the expression should be the only value left on the stack. For tracing applications, `trace` bytecodes in the expression will have recorded the necessary data, and the value on the stack may be discarded. For other applications, like conditional breakpoints, the value may be useful.

> 当字节码解释器到达表达式的末尾时，表达式的值应该是堆栈中唯一剩下的值。对于跟踪应用，表达式中的`trace`字节码将记录必要的数据，堆栈上的值可以被丢弃。对于其他应用，如条件断点，该值可能是有用的。

Separate from the stack, the interpreter has two registers:

`pc`

:   The address of the next bytecode to execute.

`start`


:   The address of the start of the bytecode expression, necessary for interpreting the `goto` and `if_goto` instructions.

> 字节码表达式开始的地址，用于解释`goto`和`if_goto`指令所必需的。


Neither of these registers is directly visible to the bytecode language itself, but they are useful for defining the meanings of the bytecode operations.

> 这两个寄存器本身对字节码语言来说不是直接可见的，但它们对定义字节码操作的含义很有用。


There are no instructions to perform side effects on the running program, or call the program's functions; we assume that these expressions are only used for unobtrusive debugging, not for patching the running code.

> 没有指示对正在运行的程序执行副作用或调用程序的函数；我们假设这些表达式仅用于不引起注意的调试，而不是用于修补正在运行的代码。


Most bytecode instructions do not distinguish between the various sizes of values, and operate on full-width values; the upper bits of the values are simply ignored, since they do not usually make a difference to the value computed. The exceptions to this rule are:

> 大多数字节码指令不区分不同大小的值，并对完整宽度的值进行操作；这些值的上位位置被忽略，因为它们通常不会影响计算的值。对此规则的例外是：

memory reference instructions (`ref``n`)


:   There are distinct instructions to fetch different word sizes from memory. Once on the stack, however, the values are treated as full-size integers. They may need to be sign-extended; the `ext` instruction exists for this purpose.

> 有不同的指令从内存获取不同大小的单词。一旦在堆栈上，这些值将被视为完整大小的整数。它们可能需要符号扩展；为此，`ext`指令存在。

the sign-extension instruction (`ext` `n`)


:   These clearly need to know which portion of their operand is to be extended to occupy the full length of the word.

> 这些显然需要知道哪一部分操作数要扩展到占据整个字的长度。


If the interpreter is unable to evaluate an expression completely for some reason (a memory location is inaccessible, or a divisor is zero, for example), we say that interpretation "terminates with an error". This means that the problem is reported back to the interpreter's caller in some helpful way. In general, code using agent expressions should assume that they may attempt to divide by zero, fetch arbitrary memory locations, and misbehave in other ways.

> 如果解释器由于某种原因无法完全评估表达式（例如无法访问内存位置或除数为零），我们就说解释“以错误终止”。这意味着将问题以某种有用的方式反馈给解释器的调用者。通常，使用代理表达式的代码应该假设它们可能会尝试除以零，访问任意内存位置，并以其他方式出现不当行为。


Even complicated C expressions compile to a few bytecode instructions; for example, the expression `x + y * z` would typically produce code like the following, assuming that `x` and `y` live in registers, and `z` is a global variable holding a 32-bit `int`:

> 即使复杂的C表达式也可以编译成几条字节码指令；例如，表达式 `x + y * z` 通常会产生如下代码，假设 `x` 和 `y` 存储在寄存器中，而 `z` 是一个全局变量，存储一个32位 `int`：

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

> 从堆栈顶部的地址获取一个32位字；用值替换堆栈中的地址。因此，我们用`z`的值替换`z`的地址。

`ext 32`


:   Sign-extend the value on the top of the stack from 32 bits to full length. This is necessary because `z` is a signed integer.

> 将栈顶的值从32位扩展到完整长度。这是必要的，因为`z`是一个有符号整数。

`mul`


:   Pop the top two numbers on the stack, multiply them, and push their product. Now the top of the stack contains the value of the expression `y * z`.

> 弹出堆栈顶部的两个数字，将它们相乘，并将它们的乘积压入堆栈。现在堆栈的顶部包含表达式`y * z`的值。

`add`


:   Pop the top two numbers, add them, and push the sum. Now the top of the stack contains the value of `x + y * z`.

> 弹出顶部的两个数字，将它们相加，并将和压入栈中。现在栈顶包含的值为`x + y * z`。

`end`


:   Stop executing; the value left on the stack top is the value to be recorded.

> 停止执行，堆栈顶部的值将被记录。

---

::: header
Next: [Bytecode Descriptions](Bytecode-Descriptions.html#Bytecode-Descriptions)]
:::
