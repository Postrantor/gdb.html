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

::: smallexample

```bash
struct timeval {
    time_t tv_sec;  /* second */
    long   tv_usec; /* microsecond */
};
```

:::

The integral datatypes conform to the definitions given in the appropriate section (see [Integral Datatypes](Integral-Datatypes.html#Integral-Datatypes), for details) so this structure is of size 8 bytes.
