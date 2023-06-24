---
tip: translate by openai@2023-06-23 21:09:47
...
---
description: File-I/O Examples (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: File-I/O Examples (Debugging with GDB)
lang: en
resource-type: document
title: File-I/O Examples (Debugging with GDB)
---
::: header
Previous: [Constants](Constants.html#Constants)]
:::

---

#### E.13.10 File-I/O Examples


Example sequence of a write call, file descriptor 3, buffer is at target address 0x1234, 6 bytes should be written:

> 示例写调用的序列，文件描述符3，缓冲区位于目标地址0x1234，应写入6个字节：

::: smallexample

```bash
<- Fwrite,3,1234,6
request memory read from target
-> m1234,6
<- XXXXXX
return "6 bytes written"
-> F6
```

:::


Example sequence of a read call, file descriptor 3, buffer is at target address 0x1234, 6 bytes should be read:

> 示例读取调用序列，文件描述符为3，缓冲区位于目标地址0x1234，应读取6个字节：

::: smallexample

```bash
<- Fread,3,1234,6
request memory write to target
-> X1234,6:XXXXXX
return "6 bytes read"
-> F6
```

:::


Example sequence of a read call, call fails on the host due to invalid file descriptor (`EBADF`):

> 例如，由於無效的文件描述符（`EBADF`）而導致對主機上的讀取調用失敗的調用序列：

::: smallexample

```bash
<- Fread,3,1234,6
-> F-1,9
```

:::


Example sequence of a read call, user presses [Ctrl-c] before syscall on host is called:

> 示例读调用序列，用户在主机上调用系统调用之前按下[Ctrl-c]：

::: smallexample

```bash
<- Fread,3,1234,6
-> F-1,4,C
<- T02
```

:::


Example sequence of a read call, user presses [Ctrl-c] after syscall on host is called:

> 示例读取调用序列：在主机上调用系统调用后，用户按下[Ctrl-c]。

::: smallexample

```bash
<- Fread,3,1234,6
-> X1234,6:XXXXXX
<- T02
```

:::
