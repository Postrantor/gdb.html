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
:::

---

#### C.6.1 Installed System-wide Configuration Scripts

The `system-gdbinit`. Otherwise, any user should be able to source them by hand as needed.

The following scripts are currently available:

- `elinos.py`' variables appropriately.
- `wrs-linux.py` This script is useful when debugging a program on a target running Wind River Linux. It expects the `ENV_PREFIX` to be set to the host-side sysroot used by the target system.
