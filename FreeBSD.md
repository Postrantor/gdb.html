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

For example, FreeBSD 12 introduced a new variant of the `kevent` system call and catching the `kevent` system call by name catches both variants:

::: smallexample

```bash
(gdb) catch syscall kevent
Catchpoint 1 (syscalls 'freebsd11_kevent' [363] 'kevent' [560])
(gdb)
```

:::
