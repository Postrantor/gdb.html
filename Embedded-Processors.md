---
tip: translate by openai@2023-06-23 20:49:30
...
---
description: Embedded Processors (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Embedded Processors (Debugging with GDB)
lang: en
resource-type: document
title: Embedded Processors (Debugging with GDB)
---
::: header
Next: [Architectures](Architectures.html#Architectures)]
:::

---

### 21.3 Embedded Processors


This section goes into details specific to particular embedded configurations.

> 这一节将详细介绍特定嵌入式配置的细节。


Whenever a specific embedded processor has a simulator, [GDB] allows to send an arbitrary command to the simulator.

> 每当一个特定的嵌入式处理器有一个模拟器时，[GDB]允许向模拟器发送任意命令。

`sim command`

:

```
Send an arbitrary `command` string to the simulator. Consult the documentation for the specific simulator in use for information about acceptable commands.
```

---


• [ARC](ARC.html#ARC):                                               Synopsys ARC

> • [ARC](ARC.html#ARC): 招募  Synopsys ARC
• [ARM](ARM.html#ARM):                                               ARM
• [BPF](BPF.html#BPF):                                               eBPF

• [M68K](M68K.html#M68K):                                            Motorola M68K

> • [M68K](M68K.html#M68K):                                     Motorola M68K（摩托罗拉M68K）

• [MicroBlaze](MicroBlaze.html#MicroBlaze):                          Xilinx MicroBlaze

> • [MicroBlaze](MicroBlaze.html#MicroBlaze):                          Xilinx MicroBlaze

• [MicroBlaze](MicroBlaze.html#MicroBlaze):                          Xilinx 微处理器

• [MIPS Embedded](MIPS-Embedded.html#MIPS-Embedded):                 MIPS Embedded

> • [MIPS 嵌入式](MIPS-Embedded.html#MIPS-Embedded):                 MIPS 嵌入式

• [OpenRISC 1000](OpenRISC-1000.html#OpenRISC-1000):                 OpenRISC 1000 (or1k)

> • [OpenRISC 1000](OpenRISC-1000.html#OpenRISC-1000):           OpenRISC 1000（or1k）

• [PowerPC Embedded](PowerPC-Embedded.html#PowerPC-Embedded):        PowerPC Embedded

> • [PowerPC 嵌入式](PowerPC-Embedded.html#PowerPC-Embedded):        PowerPC 嵌入式

• [AVR](AVR.html#AVR):                                               Atmel AVR

> • [AVR](AVR.html#AVR): 招募 Atmel AVR

• [CRIS](CRIS.html#CRIS):                                                           CRIS

> • [CRIS](CRIS.html#CRIS): CRIS

• [CRIS](CRIS.html#CRIS): CRIS

• [Super-H](Super_002dH.html#Super_002dH):                                          Renesas Super-H

> • [超級H](Super_002dH.html#Super_002dH):                                   Renesas 超級H

---
