---
tip: translate by openai@2023-06-23 23:10:54
...
---
description: How Overlays Work (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: How Overlays Work (Debugging with GDB)
lang: en
resource-type: document
title: How Overlays Work (Debugging with GDB)
---
::: header
Next: [Overlay Commands](Overlay-Commands.html#Overlay-Commands)]
:::

---

### 14.1 How Overlays Work


Suppose you have a computer whose instruction address space is only 64 kilobytes long, but which has much more memory which can be accessed by other means: special instructions, segment registers, or memory management hardware, for example. Suppose further that you want to adapt a program which is larger than 64 kilobytes to run on this system.

> 假设你有一台计算机，它的指令地址空间只有64KB，但它有更多的内存可以通过其他方式访问：特殊指令、段寄存器或内存管理硬件等。假设你想将大于64KB的程序改编，以在该系统上运行。


One solution is to identify modules of your program which are relatively independent, and need not call each other directly; call these modules *overlays*. Separate the overlays from the main program, and place their machine code in the larger memory. Place your main program in instruction memory, but leave at least enough space there to hold the largest overlay as well.

> 一个解决方案是识别你的程序的相对独立的模块，它们不需要直接相互调用；将这些模块称为*叠加*。将叠加从主程序中分离出来，将它们的机器代码放在更大的内存中。将你的主程序放在指令内存中，但至少要留出足够的空间来容纳最大的叠加。


Now, to call a function located in an overlay, you must first copy that overlay's machine code from the large memory into the space set aside for it in the instruction memory, and then jump to its entry point there.

> 现在，要调用位于叠加文件中的函数，必须首先将该叠加文件的机器码从大内存复制到指令存储器中专门为它设置的空间中，然后跳转到其入口点。

::: smallexample

```bash
    Data             Instruction            Larger
Address Space       Address Space        Address Space
+-----------+       +-----------+        +-----------+
|           |       |           |        |           |
+-----------+       +-----------+        +-----------+<-- overlay 1
| program   |       |   main    |   .----| overlay 1 | load address
| variables |       |  program  |   |    +-----------+
| and heap  |       |           |   |    |           |
+-----------+       |           |   |    +-----------+<-- overlay 2
|           |       +-----------+   |    |           | load address
+-----------+       |           |   |  .-| overlay 2 |
                    |           |   |  | |           |
         mapped --->+-----------+   |  | +-----------+
         address    |           |   |  | |           |
                    |  overlay  | <-'  | |           |
                    |   area    |  <---' +-----------+<-- overlay 3
                    |           | <---.  |           | load address
                    +-----------+     `--| overlay 3 |
                    |           |        |           |
                    +-----------+        |           |
                                         +-----------+
                                         |           |
                                         +-----------+

                    A code overlay
```

:::


The diagram (see [A code overlay](#A-code-overlay)) shows a system with separate data and instruction address spaces. To map an overlay, the program copies its code from the larger address space to the instruction address space. Since the overlays shown here all use the same mapped address, only one may be mapped at a time. For a system with a single address space for data and instructions, the diagram would be similar, except that the program variables and heap would share an address space with the main program and the overlay area.

> 图（见[A code overlay]（＃A-code-overlay））显示了一个具有单独数据和指令地址空间的系统。为了映射覆盖，程序从较大的地址空间复制其代码到指令地址空间。由于这里显示的覆盖使用相同的映射地址，因此只能映射一次。对于具有单个地址空间的数据和指令系统，图表类似，只是程序变量和堆与主程序和覆盖区共享一个地址空间。


An overlay loaded into instruction memory and ready for use is called a *mapped* overlay; its *mapped address* is its address in the instruction memory. An overlay not present (or only partially present) in instruction memory is called *unmapped*; its *load address* is its address in the larger memory. The mapped address is also called the *virtual memory address*, or *VMA*; the load address is also called the *load memory address*, or *LMA*.

> 一个已经加载到指令存储器并准备使用的叠加是称为映射叠加；其映射地址是其在指令存储器中的地址。没有（或只有部分）存在于指令存储器中的叠加被称为未映射叠加；其加载地址是其在更大的存储器中的地址。映射地址也被称为虚拟存储器地址（VMA）；加载地址也被称为加载存储器地址（LMA）。


Unfortunately, overlays are not a completely transparent way to adapt a program to limited instruction memory. They introduce a new set of global constraints you must keep in mind as you design your program:

> 不幸的是，覆盖不是一种完全透明的方式来适应有限指令存储器的程序。它们引入了一组新的全局约束，您必须牢记，在设计程序时。


- Before calling or returning to a function in an overlay, your program must make sure that overlay is actually mapped. Otherwise, the call or return will transfer control to the right address, but in the wrong overlay, and your program will probably crash.

> 在覆盖中调用或返回函数之前，您的程序必须确保覆盖实际映射。否则，调用或返回将控制权转移到正确的地址，但在错误的覆盖下，您的程序可能会崩溃。

- If the process of mapping an overlay is expensive on your system, you will need to choose your overlays carefully to minimize their effect on your program's performance.

> 如果在您的系统上将覆盖图进行映射的过程很昂贵，您将需要仔细选择覆盖图以最大限度地减少它们对您的程序性能的影响。

- The executable file you load onto your system must contain each overlay's instructions, appearing at the overlay's load address, not its mapped address. However, each overlay's instructions must be relocated and its symbols defined as if the overlay were at its mapped address. You can use GNU linker scripts to specify different load and relocation addresses for pieces of your program; see [Overlay Description](http://sourceware.org/binutils/docs/ld/Overlay-Description.html#Overlay-Description) in Using ld: the GNU linker.

> 所加载到系统上的可执行文件必须包含每个覆盖层的指令，出现在覆盖层的加载地址，而不是它的映射地址。但是，每个覆盖层的指令必须重定位，其符号必须定义为覆盖层位于其映射地址上。您可以使用GNU链接器脚本为程序的不同部分指定不同的加载和重定位地址；请参阅[Overlay Description](http://sourceware.org/binutils/docs/ld/Overlay-Description.html#Overlay-Description)，在使用ld：GNU链接器中。

- The procedure for loading executable files onto your system must be able to load their contents into the larger address space as well as the instruction and data spaces.

> 系统上加载可执行文件的程序必须能够将其内容加载到更大的地址空间以及指令和数据空间中。


The overlay system described above is rather simple, and could be improved in many ways:

> 上述描述的叠加系统相当简单，可以有很多方式改进：


- If your system has suitable bank switch registers or memory management hardware, you could use those facilities to make an overlay's load area contents simply appear at their mapped address in instruction space. This would probably be faster than copying the overlay to its mapped area in the usual way.

> 如果您的系统具有合适的银行开关寄存器或内存管理硬件，您可以使用这些设施，使覆盖物的加载区内容简单地出现在指令空间中的映射地址。这可能比通常方式将覆盖物复制到其映射区域要快。

- If your overlays are small enough, you could set aside more than one overlay area, and have more than one overlay mapped at a time.

> 如果你的覆盖层足够小，你可以设置多个覆盖区域，并同时映射多个覆盖层。

- You can use overlays to manage data, as well as instructions. In general, data overlays are even less transparent to your design than code overlays: whereas code overlays only require care when you call or return to functions, data overlays require care every time you access the data. Also, if you change the contents of a data overlay, you must copy its contents back out to its load address before you can copy a different data overlay into the same mapped area.

> 你可以使用覆层来管理数据，以及指令。一般来说，数据覆层对你的设计比代码覆层更不透明：代码覆层只需在调用或返回函数时小心，而数据覆层每次访问数据时都需要小心。此外，如果更改了数据覆层的内容，则必须将其内容复制回其加载地址，然后才能将不同的数据覆层复制到同一映射区域中。

---

::: header
Next: [Overlay Commands](Overlay-Commands.html#Overlay-Commands)]
:::
