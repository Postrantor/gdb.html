---
tip: translate by openai@2023-06-24 01:48:59
...
---
description: Rationale (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Rationale (Debugging with GDB)
lang: en
resource-type: document
title: Rationale (Debugging with GDB)
---
::: header
Previous: [Varying Target Capabilities](Varying-Target-Capabilities.html#Varying-Target-Capabilities)]
:::

---

### F.5 Rationale

Some of the design decisions apparent above are arguable.

**What about stack overflow/underflow?**


:   GDB should be able to query the target to discover its stack size. Given that information, GDB can determine at translation time whether a given expression will overflow the stack. But this spec isn't about what kinds of error-checking GDB ought to do.

> GDB应该能够查询目标以发现其堆栈大小。鉴于这些信息，GDB可以在翻译时期决定给定表达式是否会溢出堆栈。但是这个规范并不是关于GDB应该做出什么样的错误检查。

**Why are you doing everything in LONGEST?**


:   Speed isn't important, but agent code size is; using LONGEST brings in a bunch of support code to do things like division, etc. So this is a serious concern.

> 速度不重要，但代理代码大小很重要；使用LONGEST会带来大量的支持代码来做像除法等事情。因此，这是一个严重的问题。

```
First, note that you don't need different bytecodes for different operand sizes. You can generate code without *knowing* how big the stack elements actually are on the target. If the target only supports 32-bit ints, and you don't send any 64-bit bytecodes, everything just works. The observation here is that the MIPS and the Alpha have only fixed-size registers, and you can still get C's semantics even though most instructions only operate on full-sized words. You just need to make sure everything is properly sign-extended at the right times. So there is no need for 32- and 64-bit variants of the bytecodes. Just implement everything using the largest size you support.

GDB should certainly check to see what sizes the target supports, so the user can get an error earlier, rather than later. But this information is not necessary for correctness.
```

**Why don't you have `>` or `<=` operators?**


:   I want to keep the interpreter small, and we don't need them. We can combine the `less_` opcodes with `log_not`, and swap the order of the operands, yielding all four asymmetrical comparison operators. For example, `(x <= y)` is `! (x > y)`, which is `! (y < x)`.

> 我想保持解释器小巧，我们不需要它们。我们可以将`less_`操作码与`log_not`结合使用，并交换操作数的顺序，从而产生四个不对称的比较运算符。例如，`(x <= y)`是`! (x > y)`，即`! (y < x)`。

**Why do you have `log_not`?**
**Why do you have `ext`?**
**Why do you have `zero_ext`?**


:   These are all easily synthesized from other instructions, but I expect them to be used frequently, and they're simple, so I include them to keep bytecode strings short.

> 这些都可以很容易地从其他指令合成，但我期望它们经常使用，而且它们很简单，所以我将它们包含在内以保持字节码字符串短小。

```
`log_not` is equivalent to `const8 0 equal`; it's used in half the relational operators.

`ext n` is equivalent to `const8 s-n lsh const8 s-n rsh_signed`, where `s` bytecodes when the value should be signed. See the next bulleted item.

`zero_ext n` is equivalent to `constm mask log_and`; it's used whenever we push the value of a register, because we can't assume the upper bits of the register aren't garbage.
```

**Why not have sign-extending variants of the `ref` operators?**


:   Because that would double the number of `ref` operators, and we need the `ext` bytecode anyway for accessing bitfields.

> 因为这会使`ref`操作符数量增加一倍，而我们需要`ext`字节码来访问位域。

**Why not have constant-address variants of the `ref` operators?**


:   Because that would double the number of `ref` operators again, and `const32 address ref32` is only one byte longer.

> 因为这会使`ref`操作符数量再次加倍，而`const32 address ref32`只长一个字节。

**Why do the `refn` operators have to support unaligned fetches?**


:   GDB will generate bytecode that fetches multi-byte values at unaligned addresses whenever the executable's debugging information tells it to. Furthermore, GDB does not know the value the pointer will have when GDB generates the bytecode, so it cannot determine whether a particular fetch will be aligned or not.

> GDB会根据可执行文件的调试信息生成字节码，以获取未对齐地址处的多字节值。此外，GDB在生成字节码时不知道指针将具有的值，因此无法确定特定的取值是否对齐。

```
In particular, structure bitfields may be several bytes long, but follow no alignment rules; members of packed structures are not necessarily aligned either.

In general, there are many cases where unaligned references occur in correct C code, either at the programmer's explicit request, or at the compiler's discretion. Thus, it is simpler to make the GDB agent bytecodes work correctly in all circumstances than to make GDB guess in each case whether the compiler did the usual thing.
```

**Why are there no side-effecting operators?**


:   Because our current client doesn't want them? That's a cheap answer. I think the real answer is that I'm afraid of implementing function calls. We should re-visit this issue after the present contract is delivered.

> 因为我们现在的客户不想要它们？这是一个便宜的答案。我认为真正的答案是我害怕实施函数调用。在目前的合同交付后，我们应该重新审视这个问题。

**Why aren't the `goto` ops PC-relative?**


:   The interpreter has the base address around anyway for PC bounds checking, and it seemed simpler.

> 解释器本来就有基础地址来进行PC边界检查，所以似乎更简单。

**Why is there only one offset size for the `goto` ops?**


:   Offsets are currently sixteen bits. I'm not happy with this situation either:

> 目前偏移量为16位，我也不满意这种情况。

```
Suppose we have multiple branch ops with different offset sizes. As I generate code left-to-right, all my jumps are forward jumps (there are no loops in expressions), so I never know the target when I emit the jump opcode. Thus, I have to either always assume the largest offset size, or do jump relaxation on the code after I generate it, which seems like a big waste of time.

I can imagine a reasonable expression being longer than 256 bytes. I can't imagine one being longer than 64k. Thus, we need 16-bit offsets. This kind of reasoning is so bogus, but relaxation is pathetic.

The other approach would be to generate code right-to-left. Then I'd always know my offset size. That might be fun.
```

**Where is the function call bytecode?**

:   When we add side-effects, we should add this.

**Why does the `reg` bytecode take a 16-bit register number?**


:   Intel's IA-64 architecture has 128 general-purpose registers, and 128 floating-point registers, and I'm sure it has some random control registers.

> Intel的IA-64架构拥有128个通用寄存器和128个浮点寄存器，我敢肯定它还有一些随机控制寄存器。

**Why do we need `trace` and `trace_quick`?**


:   Because GDB needs to record all the memory contents and registers an expression touches. If the user wants to evaluate an expression `x->y->z`, the agent must record the values of `x` and `x->y` as well as the value of `x->y->z`.

> 因为GDB需要记录所有内存内容和表达式接触的寄存器。如果用户想要评估表达式`x->y->z`，代理必须记录`x`和`x->y`的值以及`x->y->z`的值。

**Don't the `trace` bytecodes make the interpreter less general?**


:   They do mean that the interpreter contains special-purpose code, but that doesn't mean the interpreter can only be used for that purpose. If an expression doesn't use the `trace` bytecodes, they don't get in its way.

> 他们的确意味着解释器包含了特定用途的代码，但这并不意味着解释器只能用于这个目的。如果一个表达式不使用`trace`字节码，它们不会妨碍它的使用。


**Why doesn't `trace_quick` consume its arguments the way everything else does?**

> 为什么`trace_quick`不像其他函数一样消耗它的参数？


:   In general, you do want your operators to consume their arguments; it's consistent, and generally reduces the amount of stack rearrangement necessary. However, `trace_quick` is a kludge to save space; it only exists so we needn't write `dup const8 SIZE trace` before every memory reference. Therefore, it's okay for it not to consume its arguments; it's meant for a specific context in which we know exactly what it should do with the stack. If we're going to have a kludge, it should be an effective kludge.

> 一般而言，你希望你的操作符消耗它们的参数; 这是一致的，并且通常会减少必要的堆栈重排量。但是，`trace_quick`是一个用于节省空间的变通方法; 它只存在于我们不必在每次内存引用之前写入`dup const8 SIZE trace`。因此，它不消耗参数是可以的; 它是为了一个特定的上下文而设计的，我们知道它应该如何处理堆栈。如果我们要有一个变通方法，它应该是有效的变通方法。

**Why does `trace16` exist?**


:   That opcode was added by the customer that contracted Cygnus for the data tracing work. I personally think it is unnecessary; objects that large will be quite rare, so it is okay to use `dup const16 size trace` in those cases.

> 那个操作码是由委托Cygnus进行数据跟踪工作的客户添加的。我个人认为这是没有必要的；这么大的对象很少见，因此在这些情况下使用`dup const16 size trace`是可以的。

```
Whatever we decide to do with `trace16`, we should at least leave opcode 0x30 reserved, to remain compatible with the customer who added it.
```

---

::: header
Previous: [Varying Target Capabilities](Varying-Target-Capabilities.html#Varying-Target-Capabilities)]
:::
