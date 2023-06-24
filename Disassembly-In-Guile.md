---
tip: translate by openai@2023-06-23 20:35:27
...
---
description: Disassembly In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Disassembly In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Disassembly In Guile (Debugging with GDB)
---
::: header
Next: [I/O Ports in Guile](I_002fO-Ports-in-Guile.html#I_002fO-Ports-in-Guile)]
:::

---

#### 23.4.3.22 Disassembly In Guile


The disassembler can be invoked from Scheme code. Furthermore, the disassembler can take a Guile port as input, allowing one to disassemble from any source, and not just target memory.

> 解码器可以从Scheme代码中调用。此外，解码器可以接受Guile端口作为输入，允许人们从任何来源而不仅仅是目标内存进行反汇编。

*


:   Return a list of disassembled instructions starting from the memory address `start-pc`.

> 返回从内存地址'start-pc'开始的拆解指令列表。

```
The optional argument `port` is `#f` then bytes are read from target memory.

The optional argument `offset` is offset by the same amount.

Example:

::: smallexample
``` smallexample
(gdb) guile (use-modules (rnrs io ports))
(gdb) guile (define pc (value->integer (parse-and-eval "$pc")))
(gdb) guile (define mem (open-memory #:start pc))
(gdb) guile (define bv (get-bytevector-n mem 10))
(gdb) guile (define bv-port (open-bytevector-input-port bv))
(gdb) guile (define arch (current-arch))
(gdb) guile (arch-disassemble arch pc #:port bv-port #:offset pc)
(((address . 4195516) (asm . "mov    $0x4005c8,%edi") (length . 5)))
```

:::

The optional arguments `size` is returned.

Each element of the returned list is an alist (associative list) with the following keys:

`address`

:   The value corresponding to this key is a Guile integer of the memory address of the instruction.

`asm`

:   The value corresponding to this key is a string value which represents the instruction with assembly language mnemonics. The assembly language flavor used is the same as that specified by the current CLI variable `disassembly-flavor`. See [Machine Code](Machine-Code.html#Machine-Code).

`length`

:   The value corresponding to this key is the length of the instruction in bytes.

```

---

::: header
Next: [I/O Ports in Guile](I_002fO-Ports-in-Guile.html#I_002fO-Ports-in-Guile)]
:::
```
