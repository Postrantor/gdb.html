---
tip: translate by openai@2023-06-23 14:13:46
...
---
description: System-wide Configuration Scripts (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: System-wide Configuration Scripts (Debugging with GDB)
lang: en
resource-type: document
title: System-wide Configuration Scripts (Debugging with GDB)
---
::: header

Up: [System-wide configuration](System_002dwide-configuration.html#System_002dwide-configuration)]

> 上：[系统级配置](System_002dwide-configuration.html#System_002dwide-configuration)]
:::

---

#### C.6.1 Installed System-wide Configuration Scripts


The `system-gdbinit`. Otherwise, any user should be able to source them by hand as needed.

> 系统GDBINIT。否则，任何用户都可以根据需要手动源它们。


The following scripts are currently available:

> 以下脚本当前可用：

- `elinos.py`' variables appropriately.

- `wrs-linux.py` This script is useful when debugging a program on a target running Wind River Linux. It expects the `ENV_PREFIX` to be set to the host-side sysroot used by the target system.

> 这个脚本在调试一个在Wind River Linux上运行的程序时很有用。它期望`ENV_PREFIX`被设置为目标系统使用的主机端sysroot。
