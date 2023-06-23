---
description: Stopping Before Main Program (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Stopping Before Main Program (Debugging with GDB)
lang: en
resource-type: document
title: Stopping Before Main Program (Debugging with GDB)
---
::: header
Next: [Ada Exceptions](Ada-Exceptions.html#Ada-Exceptions)]
:::

---

#### 15.4.10.5 Stopping at the Very Beginning

It is sometimes necessary to debug the program during elaboration, and before reaching the main procedure. As defined in the Ada Reference Manual, the elaboration code is invoked from a procedure called `adainit`. To run your program up to the beginning of elaboration, simply use the following two commands: `tbreak adainit` and `run`.
