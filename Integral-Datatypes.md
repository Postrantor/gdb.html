---
description: Integral Datatypes (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Integral Datatypes (Debugging with GDB)
lang: en
resource-type: document
title: Integral Datatypes (Debugging with GDB)
---
::: header
Next: [Pointer Values](Pointer-Values.html#Pointer-Values)]
:::

---

#### Integral Datatypes

The integral datatypes used in the system calls are `int`, `unsigned int`, `long`, `unsigned long`, `mode_t`, and `time_t`.

`int`, `unsigned int`, `mode_t` and `time_t` are implemented as 32 bit values in this protocol.

`long` and `unsigned long` are implemented as 64 bit types.

See [Limits](Limits.html#Limits), for corresponding MIN and MAX values (similar to those in `limits.h`) to allow range checking on host and target.

`time_t` datatypes are defined as seconds since the Epoch.

All integral datatypes transferred as part of a memory read or write of a structured datatype e.g. a `struct stat` have to be given in big endian byte order.
