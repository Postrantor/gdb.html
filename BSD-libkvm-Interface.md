---
tip: translate by openai@2023-06-23 18:27:48
...
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

> BSD衍生系统（FreeBSD / NetBSD / OpenBSD）具有内核内存接口，该接口提供了一致的接口，用于访问内核虚拟内存映像，包括实时系统和崩溃转储。[GDB]并连接到`kvm`目标：

::: smallexample

```bash
(gdb) target kvm
```

:::


For debugging crash dumps, provide the file name of the crash dump as an argument:

> 用于调试崩溃转储，请将崩溃转储的文件名作为参数提供：

::: smallexample

```bash
(gdb) target kvm /var/crash/bsd.0
```

:::


Once connected to the `kvm` target, the following commands are available:

> 一旦连接到`kvm`目标，以下命令可用：

`kvm pcb`


Set current context from the *Process Control Block* (PCB) address.

> 从进程控制块（PCB）地址设置当前上下文。

`kvm proc`


Set current context from proc address. This command isn't available on modern FreeBSD systems.

> 设置当前上下文从进程地址。这个命令在现代的FreeBSD系统中不可用。
