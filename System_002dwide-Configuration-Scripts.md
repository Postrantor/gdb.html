---
tip: translate by openai@2023-06-24 11:00:43
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

> 系统-gdbinit。否则，任何用户都可以根据需要手动提供它们。

The following scripts are currently available:

- `elinos.py`' variables appropriately.

- `wrs-linux.py` This script is useful when debugging a program on a target running Wind River Linux. It expects the `ENV_PREFIX` to be set to the host-side sysroot used by the target system.

> 这个脚本在调试目标系统上运行Wind River Linux时很有用。它期望`ENV_PREFIX`被设置为主机端sysroot由目标系统使用。
