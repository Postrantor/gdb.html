---
description: File Transfer (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: File Transfer (Debugging with GDB)
lang: en
resource-type: document
title: File Transfer (Debugging with GDB)
---
::: header
Next: [Server](Server.html#Server)]
:::

---

### 20.2 Sending files to a remote system

Some remote targets offer the ability to transfer files over the same connection used to communicate with [GDB]/Linux systems running `gdbserver` over a network interface. For other targets, e.g. embedded devices with only a single serial port, this may be the only way to upload or download files.

Not all remote targets support these commands.

`remote put hostfile targetfile`

Copy file `hostfile` on the target system.

`remote get targetfile hostfile`

Copy file `targetfile` on the host system.

`remote delete targetfile`

Delete `targetfile` from the target system.
