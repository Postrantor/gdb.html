---
description: DJGPP Native (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: DJGPP Native (Debugging with GDB)
lang: en
resource-type: document
title: DJGPP Native (Debugging with GDB)
---
::: header
Next: [Cygwin Native](Cygwin-Native.html#Cygwin-Native)]
:::

---

#### 21.1.3 Features for Debugging [DJGPP]

[DJGPP] programs are 32-bit protected-mode programs that use the *DPMI* (DOS Protected-Mode Interface) API to run on top of real-mode DOS systems and their emulations.

[GDB] port. This subsection describes those commands.

`info dos`

This is a prefix of [DJGPP]-specific commands which print information about the target system and important OS structures.

`info dos sysinfo`

This command displays assorted information about the underlying platform: the CPU type and features, the OS version and flavor, the DPMI version, and the available conventional and DPMI memory.

`info dos gdt`

`info dos ldt`

`info dos idt`

These 3 commands display entries from, respectively, Global, Local, and Interrupt Descriptor Tables (GDT, LDT, and IDT). The descriptor tables are data structures which store a descriptor for each segment that is currently in use. The segment's selector is an index into a descriptor table; the table entry for that index holds the descriptor's base address and limit, and its attributes and access rights.

A typical [DJGPP] program uses 3 segments: a code segment, a data segment (used for both data and the stack), and a DOS segment (which allows access to DOS/BIOS data structures and absolute addresses in conventional memory). However, the DPMI host will usually define additional segments in order to support the DPMI environment.

These commands allow to display entries from the descriptor tables. Without an argument, all entries from the specified table are displayed. An argument, which should be an integer expression, means display a single entry whose index is given by the argument. For example, here's a convenient way to display information about the debugged program's data segment:

::: smallexample

```bash
(gdb) info dos ldt $ds
```

```bash
0x13f: base=0x11970000 limit=0x0009ffff 32-Bit Data (Read/Write, Exp-up)
```

:::

This comes in handy when you want to see whether a pointer is outside the data segment's limit (i.e. *garbled*).

`info dos pde`

`info dos pte`

These two commands display entries from, respectively, the Page Directory and the Page Tables. Page Directories and Page Tables are data structures which control how virtual memory addresses are mapped into physical addresses. A Page Table includes an entry for every page of memory that is mapped into the program's address space; there may be several Page Tables, each one holding up to 4096 entries. A Page Directory has up to 4096 entries, one each for every Page Table that is currently in use.

Without an argument, [info dos pde] command means display entries from a single Page Table, the one pointed to by the specified entry in the Page Directory.

These commands are useful when your program uses *DMA* (Direct Memory Access), which needs physical addresses to program the DMA controller.

These commands are supported only with some DPMI servers.

`info dos address-pte addr`

This command displays the Page Table entry for a specified linear address. The argument `addr` is a linear address which should already have the appropriate segment's base address added to it, because this command accepts addresses which may belong to *any* segment. For example, here's how to display the Page Table entry for the page where a variable `i` is stored:

::: smallexample

```bash
(gdb) info dos address-pte __djgpp_base_address + (char *)&i
```

```bash
Page Table entry for address 0x11a00d30:
```

```bash
Base=0x02698000 Dirty Acc. Not-Cached Write-Back Usr Read-Write +0xd30
```

:::

This says that `i` is stored at offset `0xd30` from the page whose physical base address is `0x02698000`, and shows all the attributes of that page.

Note that you must cast the addresses of variables to a `char *`, since otherwise the value of `__djgpp_base_address`, the base address of all variables and functions in a [DJGPP] will add 4 times the value of `__djgpp_base_address` to the address of `i`.

Here's another example, it displays the Page Table entry for the transfer buffer:

::: smallexample

```bash
(gdb) info dos address-pte *((unsigned *)&_go32_info_block + 3)
```

```bash
Page Table entry for address 0x29110:
```

```bash
Base=0x00029000 Dirty Acc. Not-Cached Write-Back Usr Read-Write +0x110
```

:::

(The `+ 3` offset is because the transfer buffer's address is the 3rd member of the `_go32_info_block` structure.) The output clearly shows that this DPMI server maps the addresses in conventional memory 1:1, i.e. the physical (`0x00029000` + `0x110`) and linear (`0x29110`) addresses are identical.

This command is supported only with some DPMI servers.

In addition to native debugging, the DJGPP port supports remote debugging via a serial data link. The following commands are specific to remote serial debugging in the DJGPP port of [GDB].

`set com1base addr`

This command sets the base I/O port address of the `COM1` serial port.

`set com1irq irq`

This command sets the *Interrupt Request* (`IRQ`) line to use for the `COM1` serial port.

There are similar commands '`set com2base`', etc. for setting the port address and the `IRQ` lines for the other 3 COM ports.

The related commands '`show com1base`' etc. display the current settings of the base address and the `IRQ` lines used by the COM ports.

`info serial`

This command prints the status of the 4 DOS serial ports. For each port, it prints whether it's active or not, its I/O base address and IRQ number, whether it uses a 16550-style FIFO, its baudrate, and the counts of various errors encountered so far.

---

::: header
Next: [Cygwin Native](Cygwin-Native.html#Cygwin-Native)]
:::
