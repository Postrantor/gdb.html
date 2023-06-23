---
description: GDB/MI Ada Exception Information (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI Ada Exception Information (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI Ada Exception Information (Debugging with GDB)
---
::: header
Previous: [GDB/MI Thread Information](GDB_002fMI-Thread-Information.html#GDB_002fMI-Thread-Information)]
:::

---

#### 27.5.7 [GDB/MI]

Whenever a `*stopped` record is emitted because the program stopped after hitting an exception catchpoint (see [Set Catchpoints](Set-Catchpoints.html#Set-Catchpoints)), [GDB] provides that message via the `exception-message` field.
