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

Whenever a specific embedded processor has a simulator, [GDB] allows to send an arbitrary command to the simulator.

`sim command`

:

```
Send an arbitrary `command` string to the simulator. Consult the documentation for the specific simulator in use for information about acceptable commands.
```

---

• [ARC](ARC.html#ARC):                                               Synopsys ARC
• [ARM](ARM.html#ARM):                                               ARM
• [BPF](BPF.html#BPF):                                               eBPF
• [M68K](M68K.html#M68K):                                            Motorola M68K
• [MicroBlaze](MicroBlaze.html#MicroBlaze):                          Xilinx MicroBlaze
• [MIPS Embedded](MIPS-Embedded.html#MIPS-Embedded):                 MIPS Embedded
• [OpenRISC 1000](OpenRISC-1000.html#OpenRISC-1000):                 OpenRISC 1000 (or1k)
• [PowerPC Embedded](PowerPC-Embedded.html#PowerPC-Embedded):        PowerPC Embedded
• [AVR](AVR.html#AVR):                                               Atmel AVR
• [CRIS](CRIS.html#CRIS):                                                           CRIS
• [Super-H](Super_002dH.html#Super_002dH):                                          Renesas Super-H

---
