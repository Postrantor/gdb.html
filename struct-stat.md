---
tip: translate by openai@2023-06-24 03:23:09
...
---
description: struct stat (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: struct stat (Debugging with GDB)
lang: en
resource-type: document
title: struct stat (Debugging with GDB)
---
::: header
Next: [struct timeval](struct-timeval.html#struct-timeval)]
:::

---

#### struct stat


The buffer of type `struct stat` used by the target and [GDB] is defined as follows:

> 目标和[GDB]使用的`struct stat`类型的缓冲区定义如下：

::: smallexample

```bash
struct stat {
    unsigned int  st_dev;      /* device */
    unsigned int  st_ino;      /* inode */
    mode_t        st_mode;     /* protection */
    unsigned int  st_nlink;    /* number of hard links */
    unsigned int  st_uid;      /* user ID of owner */
    unsigned int  st_gid;      /* group ID of owner */
    unsigned int  st_rdev;     /* device type (if inode device) */
    unsigned long st_size;     /* total size, in bytes */
    unsigned long st_blksize;  /* blocksize for filesystem I/O */
    unsigned long st_blocks;   /* number of blocks allocated */
    time_t        st_atime;    /* time of last access */
    time_t        st_mtime;    /* time of last modification */
    time_t        st_ctime;    /* time of last change */
};
```

:::


The integral datatypes conform to the definitions given in the appropriate section (see [Integral Datatypes](Integral-Datatypes.html#Integral-Datatypes), for details) so this structure is of size 64 bytes.

> 整数数据类型符合适当部分中给出的定义（参见[整数数据类型](Integral-Datatypes.html#Integral-Datatypes)，了解详情），因此该结构的大小为64字节。


The values of several fields have a restricted meaning and/or range of values.

> 这些字段的值具有受限的含义和/或值域。

`st_dev`

:   A value of 0 represents a file, 1 the console.

`st_ino`

:   No valid meaning for the target. Transmitted unchanged.

`st_mode`


:   Valid mode bits are described in [Constants](Constants.html#Constants). Any other bits have currently no meaning for the target.

> 有效的模式位在[常量](Constants.html#Constants)中有描述。其他位对目标目前没有意义。

`st_uid`
`st_gid`
`st_rdev`

:   No valid meaning for the target. Transmitted unchanged.

`st_atime`
`st_mtime`
`st_ctime`


:   These values have a host and file system dependent accuracy. Especially on Windows hosts, the file system may not support exact timing values.

> 这些值具有主机和文件系统依赖的精度。特别是在Windows主机上，文件系统可能不支持精确的定时值。


The target gets a `struct stat` of the above representation and is responsible for coercing it to the target representation before continuing.

> 目标获得上述表示的`struct stat`，并负责在继续之前将其强制转换为目标表示。


Note that due to size differences between the host, target, and protocol representations of `struct stat` members, these members could eventually get truncated on the target.

> 注意，由于主机、目标和协议表示中的`struct stat`成员之间的大小差异，这些成员最终可能会在目标上被截断。

---

::: header
Next: [struct timeval](struct-timeval.html#struct-timeval)]
:::
