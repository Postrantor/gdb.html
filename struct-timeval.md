---
tip: translate by openai@2023-06-24 03:23:54
...
---
description: struct timeval (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: struct timeval (Debugging with GDB)
lang: en
resource-type: document
title: struct timeval (Debugging with GDB)
---
::: header
Previous: [struct stat](struct-stat.html#struct-stat)]
:::

---

#### struct timeval


The buffer of type `struct timeval` used by the File-I/O protocol is defined as follows:

> 文件I/O协议使用的`struct timeval`类型的缓冲区定义如下：

::: smallexample

```bash
struct timeval {
    time_t tv_sec;  /* second */
    long   tv_usec; /* microsecond */
};
```

:::


The integral datatypes conform to the definitions given in the appropriate section (see [Integral Datatypes](Integral-Datatypes.html#Integral-Datatypes), for details) so this structure is of size 8 bytes.

> 整数数据类型符合相应部分中给出的定义（参见[整数数据类型](Integral-Datatypes.html#Integral-Datatypes)，了解详情），因此此结构的大小为8个字节。
