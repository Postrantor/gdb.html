---
tip: translate by openai@2023-06-23 13:40:54
...
---
description: struct timeval (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: struct timeval (Debugging with GDB)
lang: en
resource-type: document
title: struct timeval (Debugging with GDB)
------------------------------------------

::: header
Previous: [struct stat](struct-stat.html#struct-stat)]
:::

---

#### struct timeval

The buffer of type `struct timeval` used by the File-I/O protocol is defined as follows:

> `struct timeval` 类型的缓冲区用于文件 I/O 协议定义如下：

::: smallexample

```bash
struct timeval {
    time_t tv_sec;  /* second */
    long   tv_usec; /* microsecond */
};
```

:::

The integral datatypes conform to the definitions given in the appropriate section (see [Integral Datatypes](Integral-Datatypes.html#Integral-Datatypes), for details) so this structure is of size 8 bytes.

> 整数数据类型符合相应部分（参见[整数数据类型](Integral-Datatypes.html#Integral-Datatypes)）的定义，因此此结构的大小为 8 个字节。
