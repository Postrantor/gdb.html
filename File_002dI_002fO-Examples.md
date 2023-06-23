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

::: smallexample

```bash
<- Fread,3,1234,6
-> F-1,9
```

:::

Example sequence of a read call, user presses [Ctrl-c] before syscall on host is called:

::: smallexample

```bash
<- Fread,3,1234,6
-> F-1,4,C
<- T02
```

:::

Example sequence of a read call, user presses [Ctrl-c] after syscall on host is called:

::: smallexample

```bash
<- Fread,3,1234,6
-> X1234,6:XXXXXX
<- T02
```

:::
