---
tip: translate by openai@2023-06-23 23:32:44
...
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

> 系统调用中使用的积分数据类型有`int`、`unsigned int`、`long`、`unsigned long`、`mode_t`和`time_t`。

`int`, `unsigned int`, `mode_t` and `time_t` are implemented as 32 bit values in this protocol.

`long` and `unsigned long` are implemented as 64 bit types.


See [Limits](Limits.html#Limits), for corresponding MIN and MAX values (similar to those in `limits.h`) to allow range checking on host and target.

> 请参阅[限制](Limits.html#Limits)，了解相应的最小值和最大值（类似于`limits.h`中的值），以允许在主机和目标上进行范围检查。

`time_t` datatypes are defined as seconds since the Epoch.


All integral datatypes transferred as part of a memory read or write of a structured datatype e.g. a `struct stat` have to be given in big endian byte order.

> 所有的整数数据类型作为结构数据类型（如struct stat）的内存读写的一部分传输时，必须以大端字节顺序给出。
