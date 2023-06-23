---
tip: translate by openai@2023-06-23 13:40:06
...
---
description: struct stat (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: struct stat (Debugging with GDB)
lang: en
resource-type: document
title: struct stat (Debugging with GDB)
---------------------------------------

::: header
Next: [struct timeval](struct-timeval.html#struct-timeval)]
:::

---

#### struct stat

The buffer of type `struct stat` used by the target and [GDB] is defined as follows:

> 目标和[GDB]使用的 `struct stat` 类型的缓冲区定义如下：

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

> 整数数据类型符合相应部分（参见[整数数据类型](Integral-Datatypes.html#Integral-Datatypes)以获取详细信息）中给出的定义，因此这个结构的大小为 64 字节。

The values of several fields have a restricted meaning and/or range of values.

> 多个字段的值有受限的含义和/或值范围。

`st_dev`

:   A value of 0 represents a file, 1 the console.

> 一个值为 0 代表文件，1 代表控制台。

`st_ino`

:   No valid meaning for the target. Transmitted unchanged.

> 没有有效的目标意义。传输未改变。

`st_mode`

:   Valid mode bits are described in [Constants](Constants.html#Constants). Any other bits have currently no meaning for the target.

> 有效的模式位置描述在[常量](Constants.html#Constants)中。其他位置目前对目标没有意义。

`st_uid`
`st_gid`
`st_rdev`

:   No valid meaning for the target. Transmitted unchanged.

> 无有效意义的目标。未经改变地传输。

`st_atime`
`st_mtime`
`st_ctime`

:   These values have a host and file system dependent accuracy. Especially on Windows hosts, the file system may not support exact timing values.

> 这些值的精确度取决于主机和文件系统。特别是在 Windows 主机上，文件系统可能不支持精确的时间值。

The target gets a `struct stat` of the above representation and is responsible for coercing it to the target representation before continuing.

> 目标获得上述表示的 `struct stat`，负责在继续之前将其强制转换为目标表示。

Note that due to size differences between the host, target, and protocol representations of `struct stat` members, these members could eventually get truncated on the target.

---

::: header
Next: [struct timeval](struct-timeval.html#struct-timeval)]
:::
