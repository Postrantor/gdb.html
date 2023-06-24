---
tip: translate by openai@2023-06-23 20:39:46
...
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

> DJGPP程序是32位保护模式程序，它们使用DPMI（DOS保护模式接口）API在真实模式DOS系统及其模拟上运行。

[GDB] port. This subsection describes those commands.

`info dos`


This is a prefix of [DJGPP]-specific commands which print information about the target system and important OS structures.

> 这是一个[DJGPP]特定命令的前缀，它可以打印有关目标系统和重要操作系统结构的信息。

`info dos sysinfo`


This command displays assorted information about the underlying platform: the CPU type and features, the OS version and flavor, the DPMI version, and the available conventional and DPMI memory.

> 这个命令显示有关底层平台的各种信息：CPU类型和功能、操作系统版本和风格、DPMI版本以及可用的常规和DPMI内存。

`info dos gdt`

`info dos ldt`

`info dos idt`


These 3 commands display entries from, respectively, Global, Local, and Interrupt Descriptor Tables (GDT, LDT, and IDT). The descriptor tables are data structures which store a descriptor for each segment that is currently in use. The segment's selector is an index into a descriptor table; the table entry for that index holds the descriptor's base address and limit, and its attributes and access rights.

> 这三个命令分别显示全局描述符表（GDT）、局部描述符表（LDT）和中断描述符表（IDT）中的条目。描述符表是一种存储当前使用段描述符的数据结构。段选择器是描述符表的索引；该索引的表项包含描述符的基地址和限制，以及其属性和访问权限。


A typical [DJGPP] program uses 3 segments: a code segment, a data segment (used for both data and the stack), and a DOS segment (which allows access to DOS/BIOS data structures and absolute addresses in conventional memory). However, the DPMI host will usually define additional segments in order to support the DPMI environment.

> 一个典型的DJGPP程序使用三个段：代码段、数据段（用于数据和堆栈）和DOS段（允许访问DOS/BIOS数据结构和常规内存中的绝对地址）。然而，DPMI主机通常会定义额外的段以支持DPMI环境。


These commands allow to display entries from the descriptor tables. Without an argument, all entries from the specified table are displayed. An argument, which should be an integer expression, means display a single entry whose index is given by the argument. For example, here's a convenient way to display information about the debugged program's data segment:

> 这些命令允许显示描述符表中的条目。没有参数，将显示指定表中的所有条目。参数应为整数表达式，表示显示其索引由参数给出的单个条目。例如，这是一种方便的方式来显示有关调试程序的数据段的信息：

::: smallexample

```bash
(gdb) info dos ldt $ds
```

```bash
0x13f: base=0x11970000 limit=0x0009ffff 32-Bit Data (Read/Write, Exp-up)
```

:::


This comes in handy when you want to see whether a pointer is outside the data segment's limit (i.e. *garbled*).

> 这在您想查看指针是否超出数据段限制（即*混乱*）时很有用。

`info dos pde`

`info dos pte`


These two commands display entries from, respectively, the Page Directory and the Page Tables. Page Directories and Page Tables are data structures which control how virtual memory addresses are mapped into physical addresses. A Page Table includes an entry for every page of memory that is mapped into the program's address space; there may be several Page Tables, each one holding up to 4096 entries. A Page Directory has up to 4096 entries, one each for every Page Table that is currently in use.

> 这两个命令分别显示页目录和页表的条目。页目录和页表是控制虚拟内存地址映射到物理地址的数据结构。一个页表包含映射到程序地址空间的每一页内存的条目；可能有几个页表，每个页表最多可以容纳4096个条目。页目录最多可以容纳4096个条目，每个条目对应当前使用的一个页表。


Without an argument, [info dos pde] command means display entries from a single Page Table, the one pointed to by the specified entry in the Page Directory.

> 没有参数，[info dos pde]命令意味着从单个页表中显示条目，该条目由页目录中指定的条目指向。


These commands are useful when your program uses *DMA* (Direct Memory Access), which needs physical addresses to program the DMA controller.

> 这些命令在程序使用*DMA*（直接存储器访问）时很有用，因为它需要物理地址来编程DMA控制器。

These commands are supported only with some DPMI servers.

`info dos address-pte addr`


This command displays the Page Table entry for a specified linear address. The argument `addr` is a linear address which should already have the appropriate segment's base address added to it, because this command accepts addresses which may belong to *any* segment. For example, here's how to display the Page Table entry for the page where a variable `i` is stored:

> 这个命令显示指定线性地址的页表条目。参数`addr`是一个线性地址，应该已经添加了适当段的基地址，因为这个命令接受可能属于*任何*段的地址。例如，这里是如何显示变量`i`存储的页面的页表条目：

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

> 这表明`i`存储在物理基地址为`0x02698000`的页面的偏移量`0xd30`处，并显示该页面的所有属性。


Note that you must cast the addresses of variables to a `char *`, since otherwise the value of `__djgpp_base_address`, the base address of all variables and functions in a [DJGPP] will add 4 times the value of `__djgpp_base_address` to the address of `i`.

> 注意，你必须将变量的地址强制转换为`char *`，因为否则[DJGPP]中所有变量和函数的基地址`__djgpp_base_address`的值会给`i`的地址加上4倍`__djgpp_base_address`的值。


Here's another example, it displays the Page Table entry for the transfer buffer:

> 这是另一个例子，它显示了传输缓冲区的页表条目：

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

> (`+ 3` 偏移量是因为传输缓冲区的地址是`_go32_info_block`结构的第3个成员。) 输出清楚地显示，这个DPMI服务器将常规内存中的地址1:1映射，即物理（`0x00029000` + `0x110`）和线性（`0x29110`）地址是相同的。

This command is supported only with some DPMI servers.


In addition to native debugging, the DJGPP port supports remote debugging via a serial data link. The following commands are specific to remote serial debugging in the DJGPP port of [GDB].

> 除了本地调试外，DJGPP端口还支持通过串行数据链路进行远程调试。以下命令特定于[GDB]中的DJGPP端口的远程串行调试。

`set com1base addr`

This command sets the base I/O port address of the `COM1` serial port.

`set com1irq irq`


This command sets the *Interrupt Request* (`IRQ`) line to use for the `COM1` serial port.

> 这个命令设置用于COM1串口的中断请求（IRQ）线。


There are similar commands '`set com2base`', etc. for setting the port address and the `IRQ` lines for the other 3 COM ports.

> 有类似的命令`set com2base`等用于设置其他3个COM端口的端口地址和IRQ线。


The related commands '`show com1base`' etc. display the current settings of the base address and the `IRQ` lines used by the COM ports.

> 相关命令 'show com1base' 等显示COM端口当前使用的基地址和IRQ线路的设置。

`info serial`


This command prints the status of the 4 DOS serial ports. For each port, it prints whether it's active or not, its I/O base address and IRQ number, whether it uses a 16550-style FIFO, its baudrate, and the counts of various errors encountered so far.

> 这个命令打印4个DOS串行端口的状态。对于每个端口，它会打印它是否活动，它的I/O基地址和IRQ号，是否使用16550样式的FIFO，它的波特率以及到目前为止遇到的各种错误的计数。

---

::: header
Next: [Cygwin Native](Cygwin-Native.html#Cygwin-Native)]
:::
