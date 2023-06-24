---
tip: translate by openai@2023-06-23 17:18:37
...
---
description: ARC Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: ARC Features (Debugging with GDB)
lang: en
resource-type: document
title: ARC Features (Debugging with GDB)
---
::: header
Next: [ARM Features](ARM-Features.html#ARM-Features)]
:::

---

#### G.5.2 ARC Features


ARC processors are so configurable that even core registers and their numbers are not predetermined completely. Moreover, *flags* and *PC* registers, which are important to [GDB]'.

> ARC处理器配置灵活，以至于核心寄存器及其数量都不是完全预定的。此外，*标志*和*PC*寄存器对[GDB]来说是非常重要的。


The '`org.gnu.gdb.arc.core`' feature is required for all targets. It must contain registers:

> 要求所有目标都必须包含`org.gnu.gdb.arc.core`功能，它必须包含寄存器。

- \- '`r0`' for normal register file targets.
- \- '`r0`' for reduced register file targets.
- \- '`gp`'.


In case of an ARCompact target (ARCv1 ISA), the '`org.gnu.gdb.arc.core`' registers is because of their inaccessibility during user space debugging sessions.

> 在ARCompact目标（ARCv1 ISA）的情况下，'org.gnu.gdb.arc.core'寄存器是因为在用户空间调试会话期间无法访问它们。


Extension core registers '`r32`' are optional and their existence depends on the configuration. When debugging GNU/Linux applications, i.e. user space debugging, these core registers are not available.

> 扩展内核寄存器“r32”是可选的，它们的存在取决于配置。在调试GNU/Linux应用程序时，即用户空间调试时，这些内核寄存器是不可用的。


The '`org.gnu.gdb.arc.aux`' feature is required for all ARC targets. Here is the list of registers pertinent to this feature:

> `org.gnu.gdb.arc.aux`功能对于所有ARC目标都是必需的。以下是与此功能相关的寄存器列表：

- \- mandatory: '`pc`'.
- \- optional: '`lp_start`'.

::: footnote

---

#### Footnotes

### [(23)](#DOCF23)


Not necessary for ARCv1.

> 不需要ARCv1。
:::
