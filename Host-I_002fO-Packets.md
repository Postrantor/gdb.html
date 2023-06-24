---
tip: translate by openai@2023-06-23 23:09:50
...
---
description: Host I/O Packets (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Host I/O Packets (Debugging with GDB)
lang: en
resource-type: document
title: Host I/O Packets (Debugging with GDB)
---
::: header
Next: [Interrupts](Interrupts.html#Interrupts)]
:::

---

### E.7 Host I/O Packets


The *Host I/O* packets allow [GDB], and the target's memory is not involved. See [File-I/O Remote Protocol Extension](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension), for more details on the target-initiated protocol.

> 主机I/O数据包允许[GDB]，而目标的内存不参与。有关目标发起协议的更多详细信息，请参阅[文件I/O远程协议扩展](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension)。


The Host I/O request packets all encode a single operation along with its arguments. They have this format:

> 主机I/O请求数据包都编码一个操作及其参数。它们具有以下格式：

'`vFile:operation: parameter…`'


:   `operation` depends on the operation. Numbers are always passed in hexadecimal. Negative numbers have an explicit minus sign (i.e. two's complement is not used). Strings (e.g. filenames) are encoded as a series of hexadecimal bytes. The last argument to a system call may be a buffer of escaped binary data (see [Binary Data](Overview.html#Binary-Data)).

> 操作取决于操作。数字总是以十六进制形式传递。负数具有明确的减号（即不使用二进制补码）。字符串（例如文件名）被编码为一系列十六进制字节。系统调用的最后一个参数可以是一个转义二进制数据的缓冲区（参见[Binary Data](Overview.html#Binary-Data)）。

The valid responses to Host I/O packets are:

'`F result [, errno] [; attachment]`'

:   `result`.

'``'

:   An empty response indicates that this operation is not recognized.

These are the supported Host I/O operations:

'`vFile:open: filename, flags, mode`'


:   Open a file at `filename` is an integer indicating a mask of mode bits to use if the file is created (see [mode_t Values](mode_005ft-Values.html#mode_005ft-Values)). See [open](open.html#open), for details of the open flags and mode values.

> 打开文件`filename`时，需要指定一个整数，表示如果文件需要创建时使用的模式位掩码（详见[mode_t 值](mode_005ft-Values.html#mode_005ft-Values)）。更多有关打开标志和模式值的细节，请参阅[open](open.html#open)。

'`vFile:close: fd`'


:   Close the open file corresponding to `fd` and return 0, or -1 if an error occurs.

> 关闭与`fd`相对应的打开文件，如果发生错误，则返回0或-1。

'`vFile:pread: fd, count, offset`'

:   Read data from the open file corresponding to `fd` was zero.

```
The data read should be returned as a binary attachment on success. If zero bytes were read, the response should include an empty binary attachment (i.e. a trailing semicolon). The return value is the number of target bytes read; the binary attachment may be longer if some characters were escaped.
```

'`vFile:pwrite: fd, offset, data`'

:   Write `data`, or -1 if an error occurred.

'`vFile:fstat: fd`'


:   Get information about the open file corresponding to `fd`. On success the information is returned as a binary attachment and the return value is the size of this attachment in bytes. If an error occurs the return value is -1. The format of the returned binary attachment is as described in [struct stat](struct-stat.html#struct-stat).

> 获取有关与`fd`对应的打开文件的信息。成功时，信息将以二进制附件的形式返回，返回值为此附件的大小（以字节为单位）。如果发生错误，则返回值为-1。返回的二进制附件的格式如[struct stat](struct-stat.html#struct-stat)中所述。

'`vFile:unlink: filename`'

:   Delete the file at `filename` is a string.

'`vFile:readlink: filename`'


:   Read value of symbolic link `filename` on the target. Return the number of bytes read, or -1 if an error occurs.

> 读取目标上的符号链接`文件名`的值。返回读取的字节数，如果出现错误则返回-1。

```
The data read should be returned as a binary attachment on success. If zero bytes were read, the response should include an empty binary attachment (i.e. a trailing semicolon). The return value is the number of target bytes read; the binary attachment may be longer if some characters were escaped.
```

'`vFile:setfs: pid`'


:   Select the filesystem on which `vFile` operations with `filename` to be able to access files on remote targets where the remote stub does not share a common filesystem with the inferior(s).

> 选择文件系统，以便使用`vFile`操作`filename`，以便能够访问远程目标上的文件，其中远程存根与下级没有共享的公共文件系统。

```
If `pid` is zero, select the filesystem as seen by the remote stub. Return 0 on success, or -1 if an error occurs. If `vFile:setfs:` indicates success, the selected filesystem remains selected until the next successful `vFile:setfs:` operation.
```

---

::: header
Next: [Interrupts](Interrupts.html#Interrupts)]
:::
