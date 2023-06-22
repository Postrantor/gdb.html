---
description: AArch64 (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: AArch64 (Debugging with GDB)
lang: en
resource-type: document
title: AArch64 (Debugging with GDB)
---
::: header
Next: [i386](i386.html#i386)]
:::

---

#### 21.4.1 AArch64

When [GDB] is debugging the AArch64 architecture, it provides the following special commands:

`set debug aarch64`

:

```
This command determines whether AArch64 architecture-specific debugging messages are to be displayed.
```

`show debug aarch64`

:   Show whether AArch64 debugging messages are displayed.

#### 21.4.1.1 AArch64 SVE.

When [GDB] will provide the vector registers `$z0` through `$z31`, vector predicate registers `$p0` through `$p15`, and the `$ffr` register. In addition, the pseudo register `$vg` will be provided. This is the vector granule for the current thread and represents the number of 64-bit chunks in an SVE `z` register.

If the vector length changes, then the `$vg` register will be updated, but the lengths of the `z` and `p` registers will not change. This is a known limitation of [GDB] and does not affect the execution of the target process.

#### 21.4.1.2 AArch64 Pointer Authentication.

When [GDB] is debugging the AArch64 architecture, and the program is using the v8.3-A feature Pointer Authentication (PAC), then whenever the link register `$lr` is pointing to an PAC function its value will be masked. When GDB prints a backtrace, any addresses that required unmasking will be postfixed with the marker \[PAC]. When using the MI, this is printed as part of the `addr_flags` field.

#### 21.4.1.3 AArch64 Memory Tagging Extension.

When [GDB] will make memory tagging functionality available for inspection and editing of logical and allocation tags. See [Memory Tagging](Memory-Tagging.html#Memory-Tagging).

To aid debugging, [GDB] will output additional information when SIGSEGV signals are generated as a result of memory tag failures.

If the tag violation is synchronous, the following will be shown:

::: smallexample

```bash
Program received signal SIGSEGV, Segmentation fault
Memory tag violation while accessing address 0x0500fffff7ff8000
Allocation tag 0x1
Logical tag 0x5.
```

:::

If the tag violation is asynchronous, the fault address is not available. In this case [GDB] will show the following:

::: smallexample

```bash
Program received signal SIGSEGV, Segmentation fault
Memory tag violation
Fault address unavailable.
```

:::

A special register, `tag_ctl`, is made available through the `org.gnu.gdb.aarch64.mte` feature. This register exposes some options that can be controlled at runtime and emulates the `prctl` option `PR_SET_TAGGED_ADDR_CTRL`. For further information, see the documentation in the Linux kernel.

[GDB] supports dumping memory tag data to core files through the `gcore` command and reading memory tag data from core files generated by the `gcore` command or the Linux kernel.

When a process uses memory-mapped pages protected by memory tags (for example, AArch64 MTE), this additional information will be recorded in the core file in the event of a crash or if [GDB] generates a core file from the current process state.

The memory tag data will be used so developers can display the memory tags from a particular memory region (using the '`m`' modifier to the `x` command, using the `print` command or using the various `memory-tag` subcommands.

In the case of a crash, [GDB] will attempt to retrieve the memory tag information automatically from the core file, and will show one of the above messages depending on whether the synchronous or asynchronous mode is selected. See [Memory Tagging](Memory-Tagging.html#Memory-Tagging). See [Memory](Memory.html#Memory).

---

::: header
Next: [i386](i386.html#i386)]
:::