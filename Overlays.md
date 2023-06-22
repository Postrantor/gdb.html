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

---

• [How Overlays Work](How-Overlays-Work.html#How-Overlays-Work):                                      A general explanation of overlays.
• [Overlay Commands](Overlay-Commands.html#Overlay-Commands).
• [Automatic Overlay Debugging](Automatic-Overlay-Debugging.html#Automatic-Overlay-Debugging) can find out which overlays are mapped by asking the inferior.
• [Overlay Sample Program](Overlay-Sample-Program.html#Overlay-Sample-Program):                       A sample program using overlays.

---
