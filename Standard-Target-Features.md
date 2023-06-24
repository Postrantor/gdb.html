---
tip: translate by openai@2023-06-24 03:07:54
...
---
description: Standard Target Features (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Standard Target Features (Debugging with GDB)
lang: en
resource-type: document
title: Standard Target Features (Debugging with GDB)
---
::: header
Previous: [Enum Target Types](Enum-Target-Types.html#Enum-Target-Types)]
:::

---

### G.5 Standard Target Features


A target description must contain either no registers or all the target's registers. If the description contains no registers, then [GDB] can recognize them.

> 目标描述必须包含所有目标的寄存器或不包含任何寄存器。如果描述不包含寄存器，那么[GDB]可以识别它们。


This is accomplished by giving specific names to feature elements which contain standard registers. [GDB] will display them just as if they were added to an unrecognized feature.

> 通过给包含标准寄存器的特征元素赋予具体的名称来实现这一点。[GDB]将把它们显示出来，就好像它们被添加到一个未识别的特征一样。


This section lists the known features and their expected contents. Sample XML documents for these features are included in the [GDB].

> 这一节列出了已知的功能及其预期内容。这些功能的示例XML文档包含在[GDB]中。

Names recognized by [GDB]'.


The names of registers are not case sensitive for the purpose of recognizing standard features, but [GDB] will only display registers using the capitalization used in the description.

> 对于识别标准特性的目的，寄存器的名称不区分大小写，但[GDB]只会使用描述中使用的大写来显示寄存器。

---


• [AArch64 Features](AArch64-Features.html#AArch64-Features):                               

> • [AArch64 特性](AArch64-Features.html#AArch64-Features):

• [ARC Features](ARC-Features.html#ARC-Features):                                           

> • [ARC 特性](ARC-Features.html#ARC-Features):

• [ARM Features](ARM-Features.html#ARM-Features):                                           

> • [ARM 功能](ARM-Features.html#ARM-Features):

• [i386 Features](i386-Features.html#i386-Features):                                        

> • [i386 特性](i386-Features.html#i386-Features):

• [LoongArch Features](LoongArch-Features.html#LoongArch-Features):                         

> • [LoongArch 特征](LoongArch-Features.html#LoongArch-Features):

• [MicroBlaze Features](MicroBlaze-Features.html#MicroBlaze-Features):                      

> • [MicroBlaze 特征](MicroBlaze-Features.html#MicroBlaze-Features):

• [MIPS Features](MIPS-Features.html#MIPS-Features):                                        

> • [MIPS 特征](MIPS-Features.html#MIPS-Features):

• [M68K Features](M68K-Features.html#M68K-Features):                                        

> • [M68K 特征](M68K-Features.html#M68K-Features):

• [NDS32 Features](NDS32-Features.html#NDS32-Features):                                     

> • [NDS32 特性](NDS32-Features.html#NDS32-Features):

• [Nios II Features](Nios-II-Features.html#Nios-II-Features):                                              

> • [Nios II 特性](Nios-II-Features.html#Nios-II-Features):

• [OpenRISC 1000 Features](OpenRISC-1000-Features.html#OpenRISC-1000-Features):                            

> •[OpenRISC 1000特征](OpenRISC-1000-Features.html#OpenRISC-1000-Features): 了解

• [PowerPC Features](PowerPC-Features.html#PowerPC-Features):                                              

> • [PowerPC 特征](PowerPC-Features.html#PowerPC-Features):

• [RISC-V Features](RISC_002dV-Features.html#RISC_002dV-Features):                                         

> • [RISC-V 特性](RISC_002dV-Features.html#RISC_002dV-Features):

• [RX Features](RX-Features.html#RX-Features):                                                             

> •[RX功能](RX-Features.html#RX-Features):

• [S/390 and System z Features](S_002f390-and-System-z-Features.html#S_002f390-and-System-z-Features):     

> • [S/390 和 System z 特性](S_002f390-and-System-z-Features.html#S_002f390-and-System-z-Features):

• [Sparc Features](Sparc-Features.html#Sparc-Features):                                                    

> •[Sparc 特性](Sparc-Features.html#Sparc-Features):

• [TIC6x Features](TIC6x-Features.html#TIC6x-Features):                                                    

> • [TIC6x功能](TIC6x-Features.html#TIC6x-Features):

---

---

::: header
Previous: [Enum Target Types](Enum-Target-Types.html#Enum-Target-Types)]
:::
