---
tip: translate by openai@2023-06-23 21:31:13
...
---
description: FreeBSD (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: FreeBSD (Debugging with GDB)
lang: en
resource-type: document
title: FreeBSD (Debugging with GDB)
---
::: header
Previous: [Darwin](Darwin.html#Darwin)]
:::

---

#### 21.1.7 FreeBSD


When the ABI of a system call is changed in the FreeBSD kernel, this is implemented by leaving a compatibility system call using the old ABI at the existing number and allocating a new system call number for the version using the new ABI. As a convenience, when a system call is caught by name (see [catch syscall](Set-Catchpoints.html#catch-syscall)), compatibility system calls are also caught.

> 当FreeBSD内核中的系统调用的ABI发生变化时，会通过将使用旧ABI的兼容系统调用留在现有编号上，并为使用新ABI的版本分配新的系统调用编号来实现。为了方便，当系统调用以名称被捕获（参见[捕获系统调用](Set-Catchpoints.html#catch-syscall)）时，兼容系统调用也会被捕获。


For example, FreeBSD 12 introduced a new variant of the `kevent` system call and catching the `kevent` system call by name catches both variants:

> 例如，FreeBSD 12引入了一个新的`kevent`系统调用变体，通过名称捕获`kevent`系统调用可以捕获这两个变体。

::: smallexample

```bash
(gdb) catch syscall kevent
Catchpoint 1 (syscalls 'freebsd11_kevent' [363] 'kevent' [560])
(gdb)
```

:::
