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

One solution is to identify modules of your program which are relatively independent, and need not call each other directly; call these modules *overlays*. Separate the overlays from the main program, and place their machine code in the larger memory. Place your main program in instruction memory, but leave at least enough space there to hold the largest overlay as well.

Now, to call a function located in an overlay, you must first copy that overlay's machine code from the large memory into the space set aside for it in the instruction memory, and then jump to its entry point there.

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

An overlay loaded into instruction memory and ready for use is called a *mapped* overlay; its *mapped address* is its address in the instruction memory. An overlay not present (or only partially present) in instruction memory is called *unmapped*; its *load address* is its address in the larger memory. The mapped address is also called the *virtual memory address*, or *VMA*; the load address is also called the *load memory address*, or *LMA*.

Unfortunately, overlays are not a completely transparent way to adapt a program to limited instruction memory. They introduce a new set of global constraints you must keep in mind as you design your program:

- Before calling or returning to a function in an overlay, your program must make sure that overlay is actually mapped. Otherwise, the call or return will transfer control to the right address, but in the wrong overlay, and your program will probably crash.
- If the process of mapping an overlay is expensive on your system, you will need to choose your overlays carefully to minimize their effect on your program's performance.
- The executable file you load onto your system must contain each overlay's instructions, appearing at the overlay's load address, not its mapped address. However, each overlay's instructions must be relocated and its symbols defined as if the overlay were at its mapped address. You can use GNU linker scripts to specify different load and relocation addresses for pieces of your program; see [Overlay Description](http://sourceware.org/binutils/docs/ld/Overlay-Description.html#Overlay-Description) in Using ld: the GNU linker.
- The procedure for loading executable files onto your system must be able to load their contents into the larger address space as well as the instruction and data spaces.

The overlay system described above is rather simple, and could be improved in many ways:

- If your system has suitable bank switch registers or memory management hardware, you could use those facilities to make an overlay's load area contents simply appear at their mapped address in instruction space. This would probably be faster than copying the overlay to its mapped area in the usual way.
- If your overlays are small enough, you could set aside more than one overlay area, and have more than one overlay mapped at a time.
- You can use overlays to manage data, as well as instructions. In general, data overlays are even less transparent to your design than code overlays: whereas code overlays only require care when you call or return to functions, data overlays require care every time you access the data. Also, if you change the contents of a data overlay, you must copy its contents back out to its load address before you can copy a different data overlay into the same mapped area.

---

::: header
Next: [Overlay Commands](Overlay-Commands.html#Overlay-Commands)]
:::
