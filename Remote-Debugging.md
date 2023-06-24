---
tip: translate by openai@2023-06-24 02:04:49
...
---
description: Remote Debugging (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Remote Debugging (Debugging with GDB)
lang: en
resource-type: document
title: Remote Debugging (Debugging with GDB)
---
::: header
Next: [Configurations](Configurations.html#Configurations)]
:::

---

## 20 Debugging Remote Programs


If you are trying to debug a program running on a machine that cannot run [GDB] in the usual way, it is often useful to use remote debugging. For example, you might use remote debugging on an operating system kernel, or on a small system which does not have a general purpose operating system powerful enough to run a full-featured debugger.

> 如果您正在尝试调试在无法以通常方式运行[GDB]的机器上运行的程序，则通常有用的是使用远程调试。例如，您可以在操作系统内核上或在没有足够强大的通用操作系统来运行全功能调试器的小系统上使用远程调试。

Some configurations of [GDB].


Other remote targets may be available in your configuration of [GDB]; use `help target` to list them.

> 其他远程目标可能在您的[GDB]配置中可用；使用“help target”来列出它们。

---


• [Connecting](Connecting.html#Connecting):                                      Connecting to a remote target

> • [连接](Connecting.html#Connecting): 连接到远程目标

• [File Transfer](File-Transfer.html#File-Transfer):                             Sending files to a remote system

> • [文件传输](File-Transfer.html#File-Transfer)：将文件发送到远程系统

• [Server](Server.html#Server):                                                  Using the gdbserver program

> • [服务器](Server.html#Server)：使用 gdbserver 程序

• [Remote Configuration](Remote-Configuration.html#Remote-Configuration):        Remote configuration

> • [远程配置](Remote-Configuration.html#Remote-Configuration):     远程配置

• [Remote Stub](Remote-Stub.html#Remote-Stub):                                   Implementing a remote stub

> • [遠程存根](Remote-Stub.html#Remote-Stub)：實現遠程存根

---
