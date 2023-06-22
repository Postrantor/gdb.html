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

The protocol is defined to be independent of both the host and target systems. It uses its own internal representation of datatypes and values. Both [GDB] stub are responsible for translating the system-dependent value representations into the internal protocol representations when data is transmitted.

The communication is synchronous. A system call is possible only when [GDB].

The target's request to perform a host system call does not finish the latest '`C` is required.

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

File I/O is not supported in non-stop mode.

---

::: header
Next: [Protocol Basics](Protocol-Basics.html#Protocol-Basics)]
:::
