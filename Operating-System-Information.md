---
description: Operating System Information (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Operating System Information (Debugging with GDB)
lang: en
resource-type: document
title: Operating System Information (Debugging with GDB)
---
::: header
Next: [Trace File Format](Trace-File-Format.html#Trace-File-Format)]
:::

---

## Appendix H Operating System Information

Users of [GDB] often wish to obtain information about the state of the operating system running on the target---for example the list of processes, or the list of open files. This section describes the mechanism that makes it possible. This mechanism is similar to the target features mechanism (see [Target Descriptions](Target-Descriptions.html#Target-Descriptions)), but focuses on a different aspect of target.

Operating system information is retrieved from the target via the remote protocol, using '`qXfer` identifies the data to be fetched.

---

• [Process list](Process-list.html#Process-list):     

---
