---
tip: translate by openai@2023-06-23 14:22:45
...
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

> 使用GDB来调试嵌入式系统的挑战之一是，每种处理器架构都有很多细微的变体。厂商通常以标准处理器核心（如ARM、PowerPC或MIPS）为基础，进行改动以适应特定的市场领域。有些架构有数百种变体，来自数十家供应商。这会导致一些问题：


- With so many different customized processors, it is difficult for the [GDB] maintainers to keep up with the changes.

> 随着许多不同的定制处理器，[GDB] 维护者很难跟上变化。

- Since individual variants may have short lifetimes or limited audiences, it may not be worthwhile to carry information about every variant in the [GDB] source tree.

> 由于个体变体可能具有短暂的寿命或有限的受众，在[GDB]源树中携带有关每个变体的信息可能不值得。

- When [GDB] does support the architecture of the embedded system at hand, the task of finding the correct architecture name to give the `set architecture` command can be error-prone.

> 当[GDB]支持手头的嵌入式系统的架构时，找到正确的架构名称来给`set architecture`命令可能会出错。


To address these problems, the [GDB] understands them.

> 为了解决这些问题，[GDB]了解它们。


[GDB] must be linked with the Expat library to support XML target descriptions. See [Expat](Requirements.html#Expat).

> GDB必须与Expat库链接以支持XML目标描述。请参见[Expat](Requirements.html#Expat)。

---


• [Retrieving Descriptions](Retrieving-Descriptions.html#Retrieving-Descriptions):              How descriptions are fetched from a target.

> • [检索描述](Retrieving-Descriptions.html#Retrieving-Descriptions):              从目标处获取描述的方法。

• [Target Description Format](Target-Description-Format.html#Target-Description-Format):        The contents of a target description.

> • [目标描述格式](Target-Description-Format.html#Target-Description-Format):   内容目标描述。

• [Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types):              Standard types available for target descriptions.

> • [预定义目标类型](Predefined-Target-Types.html#Predefined-Target-Types):         标准类型可用于目标描述。

• [Enum Target Types](Enum-Target-Types.html#Enum-Target-Types):                                How to define enum target types.

> •[枚举目标类型](Enum-Target-Types.html#Enum-Target-Types)：如何定义枚举目标类型。

• [Standard Target Features](Standard-Target-Features.html#Standard-Target-Features) knows about.

> • [标准目标功能](Standard-Target-Features.html#Standard-Target-Features)知道。

---

---

::: header
Next: [Operating System Information](Operating-System-Information.html#Operating-System-Information)]
:::
