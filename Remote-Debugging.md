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

Some configurations of [GDB].

Other remote targets may be available in your configuration of [GDB]; use `help target` to list them.

---

• [Connecting](Connecting.html#Connecting):                                      Connecting to a remote target
• [File Transfer](File-Transfer.html#File-Transfer):                             Sending files to a remote system
• [Server](Server.html#Server):                                                  Using the gdbserver program
• [Remote Configuration](Remote-Configuration.html#Remote-Configuration):        Remote configuration
• [Remote Stub](Remote-Stub.html#Remote-Stub):                                   Implementing a remote stub

---
