---
tip: translate by openai@2023-06-24 00:57:17
...
---
description: Overlays (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Overlays (Debugging with GDB)
lang: en
resource-type: document
title: Overlays (Debugging with GDB)
---
::: header
Next: [Languages](Languages.html#Languages)]
:::

---

## 14 Debugging Programs That Use Overlays


If your program is too large to fit completely in your target system's memory, you can sometimes use *overlays* to work around this problem. [GDB] provides some support for debugging programs that use overlays.

> 如果你的程序太大而无法完全适配你的目标系统的内存，你有时可以使用覆盖来解决这个问题。[GDB]提供了一些支持来调试使用覆盖的程序。

---


• [How Overlays Work](How-Overlays-Work.html#How-Overlays-Work):                                      A general explanation of overlays.

> • [如何使用覆层](How-Overlays-Work.html#How-Overlays-Work): 一个关于覆层的概括性解释。
• [Overlay Commands](Overlay-Commands.html#Overlay-Commands).

• [Automatic Overlay Debugging](Automatic-Overlay-Debugging.html#Automatic-Overlay-Debugging) can find out which overlays are mapped by asking the inferior.

> • [自动覆盖调试](Automatic-Overlay-Debugging.html#Automatic-Overlay-Debugging)可以通过询问劣势来确定哪些覆盖被映射。

• [Overlay Sample Program](Overlay-Sample-Program.html#Overlay-Sample-Program):                       A sample program using overlays.

> • [示例覆盖程序](Overlay-Sample-Program.html#Overlay-Sample-Program):                       使用覆盖的示例程序。

---
