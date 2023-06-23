---
description: Target Descriptions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Target Descriptions (Debugging with GDB)
lang: en
resource-type: document
title: Target Descriptions (Debugging with GDB)
---
::: header
Next: [Operating System Information](Operating-System-Information.html#Operating-System-Information)]
:::

---

## Appendix G Target Descriptions

One of the challenges of using [GDB] to debug embedded systems is that there are so many minor variants of each processor architecture in use. It is common practice for vendors to start with a standard processor core --- ARM, PowerPC, or MIPS, for example --- and then make changes to adapt it to a particular market niche. Some architectures have hundreds of variants, available from dozens of vendors. This leads to a number of problems:

- With so many different customized processors, it is difficult for the [GDB] maintainers to keep up with the changes.
- Since individual variants may have short lifetimes or limited audiences, it may not be worthwhile to carry information about every variant in the [GDB] source tree.
- When [GDB] does support the architecture of the embedded system at hand, the task of finding the correct architecture name to give the `set architecture` command can be error-prone.

To address these problems, the [GDB] understands them.

[GDB] must be linked with the Expat library to support XML target descriptions. See [Expat](Requirements.html#Expat).

---

• [Retrieving Descriptions](Retrieving-Descriptions.html#Retrieving-Descriptions):              How descriptions are fetched from a target.
• [Target Description Format](Target-Description-Format.html#Target-Description-Format):        The contents of a target description.
• [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types):              Standard types available for target descriptions.
• [Enum Target Types](Enum-Target-Types.html#Enum-Target-Types):                                How to define enum target types.
• [Standard Target Features](Standard-Target-Features.html#Standard-Target-Features) knows about.

---

---

::: header
Next: [Operating System Information](Operating-System-Information.html#Operating-System-Information)]
:::
