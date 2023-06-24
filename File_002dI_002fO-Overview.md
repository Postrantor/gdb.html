---
tip: translate by openai@2023-06-23 21:10:20
...
---
description: File-I/O Overview (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: File-I/O Overview (Debugging with GDB)
lang: en
resource-type: document
title: File-I/O Overview (Debugging with GDB)
---
::: header
Next: [Protocol Basics](Protocol-Basics.html#Protocol-Basics)]
:::

---

#### E.13.1 File-I/O Overview


The *File I/O remote protocol extension* (short: File-I/O) allows the target to use the host's file system and console I/O to perform various system calls. System calls on the target system are translated into a remote protocol packet to the host system, which then performs the needed actions and returns a response packet to the target system. This simulates file system operations even on targets that lack file systems.

> 文件I/O远程协议扩展（简称：File-I/O）允许目标使用主机的文件系统和控制台I/O执行各种系统调用。目标系统上的系统调用会被转换为远程协议数据包发送到主机系统，然后主机系统执行所需的操作并将响应数据包发送回目标系统。即使在缺乏文件系统的目标上也能模拟文件系统操作。


The protocol is defined to be independent of both the host and target systems. It uses its own internal representation of datatypes and values. Both [GDB] stub are responsible for translating the system-dependent value representations into the internal protocol representations when data is transmitted.

> 协议被定义为独立于主机和目标系统的。它使用自己的内部数据类型和值表示。当数据被传输时，两个[GDB]存根都负责将系统相关的值表示转换为内部协议表示。


The communication is synchronous. A system call is possible only when [GDB].

> 通信是同步的。只有在[GDB]时才可以进行系统调用。


The target's request to perform a host system call does not finish the latest '`C` is required.

> 目标要求执行主机系统调用未能完成，最新版本需要`C`语言。

::: smallexample

```bash
(gdb) continue
  <- target requests 'system call X'
  target is stopped, GDB executes system call
  -> GDB returns result
  ... target continues, GDB returns to wait for the target
  <- target hits breakpoint and sends a Txx packet
```

:::


The protocol only supports I/O on the console and to regular files on the host file system. Character or block special devices, pipes, named pipes, sockets or any other communication method on the host system are not supported by this protocol.

> 此协议仅支持控制台上的I/O和主机文件系统上的常规文件。不支持主机系统上的字符或块特殊设备、管道、命名管道、套接字或任何其他通信方法。

File I/O is not supported in non-stop mode.

---

::: header
Next: [Protocol Basics](Protocol-Basics.html#Protocol-Basics)]
:::
