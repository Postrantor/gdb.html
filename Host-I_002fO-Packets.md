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

The Host I/O request packets all encode a single operation along with its arguments. They have this format:

'`vFile:operation: parameter…`'

:   `operation` depends on the operation. Numbers are always passed in hexadecimal. Negative numbers have an explicit minus sign (i.e. two's complement is not used). Strings (e.g. filenames) are encoded as a series of hexadecimal bytes. The last argument to a system call may be a buffer of escaped binary data (see [Binary Data](Overview.html#Binary-Data)).

The valid responses to Host I/O packets are:

'`F result [, errno] [; attachment]`'

:   `result`.

'``'

:   An empty response indicates that this operation is not recognized.

These are the supported Host I/O operations:

'`vFile:open: filename, flags, mode`'

:   Open a file at `filename` is an integer indicating a mask of mode bits to use if the file is created (see [mode_t Values](mode_005ft-Values.html#mode_005ft-Values)). See [open](open.html#open), for details of the open flags and mode values.

'`vFile:close: fd`'

:   Close the open file corresponding to `fd` and return 0, or -1 if an error occurs.

'`vFile:pread: fd, count, offset`'

:   Read data from the open file corresponding to `fd` was zero.

```
The data read should be returned as a binary attachment on success. If zero bytes were read, the response should include an empty binary attachment (i.e. a trailing semicolon). The return value is the number of target bytes read; the binary attachment may be longer if some characters were escaped.
```

'`vFile:pwrite: fd, offset, data`'

:   Write `data`, or -1 if an error occurred.

'`vFile:fstat: fd`'

:   Get information about the open file corresponding to `fd`. On success the information is returned as a binary attachment and the return value is the size of this attachment in bytes. If an error occurs the return value is -1. The format of the returned binary attachment is as described in [struct stat](struct-stat.html#struct-stat).

'`vFile:unlink: filename`'

:   Delete the file at `filename` is a string.

'`vFile:readlink: filename`'

:   Read value of symbolic link `filename` on the target. Return the number of bytes read, or -1 if an error occurs.

```
The data read should be returned as a binary attachment on success. If zero bytes were read, the response should include an empty binary attachment (i.e. a trailing semicolon). The return value is the number of target bytes read; the binary attachment may be longer if some characters were escaped.
```

'`vFile:setfs: pid`'

:   Select the filesystem on which `vFile` operations with `filename` to be able to access files on remote targets where the remote stub does not share a common filesystem with the inferior(s).

```
If `pid` is zero, select the filesystem as seen by the remote stub. Return 0 on success, or -1 if an error occurs. If `vFile:setfs:` indicates success, the selected filesystem remains selected until the next successful `vFile:setfs:` operation.
```

---

::: header
Next: [Interrupts](Interrupts.html#Interrupts)]
:::
