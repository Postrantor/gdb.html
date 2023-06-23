---
description: Altering (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Altering (Debugging with GDB)
lang: en
resource-type: document
title: Altering (Debugging with GDB)
---
::: header
Next: [GDB Files](GDB-Files.html#GDB-Files)]
:::

---

## 17 Altering Execution

Once you think you have found an error in your program, you might want to find out for certain whether correcting the apparent error would lead to correct results in the rest of the run. You can find the answer by experiment, using the [GDB] features for altering execution of the program.

For example, you can store new values into variables or memory locations, give your program a signal, restart it at a different address, or even return prematurely from a function.

---

• [Assignment](Assignment.html#Assignment):                                                              Assignment to variables
• [Jumping](Jumping.html#Jumping):                                                                       Continuing at a different address
• [Signaling](Signaling.html#Signaling):                                                                 Giving your program a signal
• [Returning](Returning.html#Returning):                                                                 Returning from a function
• [Calling](Calling.html#Calling):                                                                       Calling your program's functions
• [Patching](Patching.html#Patching):                                                                    Patching your program
• [Compiling and Injecting Code](Compiling-and-Injecting-Code.html#Compiling-and-Injecting-Code)

---
