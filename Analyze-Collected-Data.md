---
description: Analyze Collected Data (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Analyze Collected Data (Debugging with GDB)
lang: en
resource-type: document
title: Analyze Collected Data (Debugging with GDB)
---
::: header
Next: [Tracepoint Variables](Tracepoint-Variables.html#Tracepoint-Variables)]
:::

---

### 13.2 Using the Collected Data

After the tracepoint experiment ends, you use [GDB] commands (`print`, `info registers`, `backtrace`, etc.) will behave as if we were currently debugging the program state as it was when the tracepoint occurred. Any requests for data that are not in the buffer will fail.

---

• [tfind](tfind.html#tfind):                                         How to select a trace snapshot
• [tdump](tdump.html#tdump):                                         How to display all data for a snapshot
• [save tracepoints](save-tracepoints.html#save-tracepoints):        How to save tracepoints for a future run

---
