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

The '`org.gnu.gdb.arc.core`' feature is required for all targets. It must contain registers:

- \- '`r0`' for normal register file targets.
- \- '`r0`' for reduced register file targets.
- \- '`gp`'.

In case of an ARCompact target (ARCv1 ISA), the '`org.gnu.gdb.arc.core`' registers is because of their inaccessibility during user space debugging sessions.

Extension core registers '`r32`' are optional and their existence depends on the configuration. When debugging GNU/Linux applications, i.e. user space debugging, these core registers are not available.

The '`org.gnu.gdb.arc.aux`' feature is required for all ARC targets. Here is the list of registers pertinent to this feature:

- \- mandatory: '`pc`'.
- \- optional: '`lp_start`'.

::: footnote

---

#### Footnotes

### [(23)](#DOCF23)

Not necessary for ARCv1.
:::
