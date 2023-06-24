---
tip: translate by openai@2023-06-23 21:01:29
...
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

> 一些遠程目標提供了在與[GDB]/Linux系統通過網絡接口通信時，可以在同一連接上傳輸文件的能力。對於其他目標，例如只有單個串口的嵌入式設備，這可能是唯一的方法來上傳或下載文件。

Not all remote targets support these commands.

`remote put hostfile targetfile`

Copy file `hostfile` on the target system.

`remote get targetfile hostfile`

Copy file `targetfile` on the host system.

`remote delete targetfile`

Delete `targetfile` from the target system.
