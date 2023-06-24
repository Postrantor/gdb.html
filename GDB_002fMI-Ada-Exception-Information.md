---
tip: translate by openai@2023-06-23 21:42:54
...
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

> 每当程序在遇到异常捕获点（参见[设置捕获点](Set-Catchpoints.html#Set-Catchpoints))后停止时，GDB就会通过`exception-message`字段发出一条`*stopped`记录。
