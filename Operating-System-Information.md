---
tip: translate by openai@2023-06-24 00:46:09
...
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

> 用户经常希望获取有关目标正在运行的操作系统状态的信息--例如进程列表或打开文件列表。本节描述了使其成为可能的机制。该机制类似于目标功能机制（参见[目标描述]（Target-Descriptions.html#Target-Descriptions）），但关注的是目标的另一个方面。


Operating system information is retrieved from the target via the remote protocol, using '`qXfer` identifies the data to be fetched.

> 从目标机器通过远程协议获取操作系统信息，使用'qXfer'标识要获取的数据。

---

• [Process list](Process-list.html#Process-list):     

---
