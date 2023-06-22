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

This is accomplished by giving specific names to feature elements which contain standard registers. [GDB] will display them just as if they were added to an unrecognized feature.

This section lists the known features and their expected contents. Sample XML documents for these features are included in the [GDB].

Names recognized by [GDB]'.

The names of registers are not case sensitive for the purpose of recognizing standard features, but [GDB] will only display registers using the capitalization used in the description.

---

• [AArch64 Features](AArch64-Features.html#AArch64-Features):                               
• [ARC Features](ARC-Features.html#ARC-Features):                                           
• [ARM Features](ARM-Features.html#ARM-Features):                                           
• [i386 Features](i386-Features.html#i386-Features):                                        
• [LoongArch Features](LoongArch-Features.html#LoongArch-Features):                         
• [MicroBlaze Features](MicroBlaze-Features.html#MicroBlaze-Features):                      
• [MIPS Features](MIPS-Features.html#MIPS-Features):                                        
• [M68K Features](M68K-Features.html#M68K-Features):                                        
• [NDS32 Features](NDS32-Features.html#NDS32-Features):                                     
• [Nios II Features](Nios-II-Features.html#Nios-II-Features):                                              
• [OpenRISC 1000 Features](OpenRISC-1000-Features.html#OpenRISC-1000-Features):                            
• [PowerPC Features](PowerPC-Features.html#PowerPC-Features):                                              
• [RISC-V Features](RISC_002dV-Features.html#RISC_002dV-Features):                                         
• [RX Features](RX-Features.html#RX-Features):                                                             
• [S/390 and System z Features](S_002f390-and-System-z-Features.html#S_002f390-and-System-z-Features):     
• [Sparc Features](Sparc-Features.html#Sparc-Features):                                                    
• [TIC6x Features](TIC6x-Features.html#TIC6x-Features):                                                    

---

---

::: header
Previous: [Enum Target Types](Enum-Target-Types.html#Enum-Target-Types)]
:::
