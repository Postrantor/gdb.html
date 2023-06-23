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

The values of several fields have a restricted meaning and/or range of values.

`st_dev`

:   A value of 0 represents a file, 1 the console.

`st_ino`

:   No valid meaning for the target. Transmitted unchanged.

`st_mode`

:   Valid mode bits are described in [Constants](Constants.html#Constants). Any other bits have currently no meaning for the target.

`st_uid`
`st_gid`
`st_rdev`

:   No valid meaning for the target. Transmitted unchanged.

`st_atime`
`st_mtime`
`st_ctime`

:   These values have a host and file system dependent accuracy. Especially on Windows hosts, the file system may not support exact timing values.

The target gets a `struct stat` of the above representation and is responsible for coercing it to the target representation before continuing.

Note that due to size differences between the host, target, and protocol representations of `struct stat` members, these members could eventually get truncated on the target.

---

::: header
Next: [struct timeval](struct-timeval.html#struct-timeval)]
:::
