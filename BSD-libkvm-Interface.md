---
description: BSD libkvm Interface (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: BSD libkvm Interface (Debugging with GDB)
lang: en
resource-type: document
title: BSD libkvm Interface (Debugging with GDB)
---
::: header
Next: [Process Information](Process-Information.html#Process-Information)]
:::

---

#### 21.1.1 BSD libkvm Interface

BSD-derived systems (FreeBSD/NetBSD/OpenBSD) have a kernel memory interface that provides a uniform interface for accessing kernel virtual memory images, including live systems and crash dumps. [GDB] and connect to the `kvm` target:

::: smallexample

```bash
(gdb) target kvm
```

:::

For debugging crash dumps, provide the file name of the crash dump as an argument:

::: smallexample

```bash
(gdb) target kvm /var/crash/bsd.0
```

:::

Once connected to the `kvm` target, the following commands are available:

`kvm pcb`

Set current context from the *Process Control Block* (PCB) address.

`kvm proc`

Set current context from proc address. This command isn't available on modern FreeBSD systems.
