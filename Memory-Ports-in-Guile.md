---
description: Memory Ports in Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Memory Ports in Guile (Debugging with GDB)
lang: en
resource-type: document
title: Memory Ports in Guile (Debugging with GDB)
---
::: header
Next: [Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile)]
:::

---

#### 23.4.3.24 Memory Ports in Guile

[GDB] provides a `port` interface to target memory. This allows Guile code to read/write target memory using Guile's port and bytevector functionality. The main routine is `open-memory` which returns a port object. One can then read/write memory using that object.

*

:   Return a port object that can be used for reading and writing memory. The port will be open according to `mode`', read-only and buffered.

```
The chunk of memory that can be accessed can be bounded. If both `start`) can be accessed.
```

```
<!-- -->
```

Scheme Procedure: **memory-port?**

:   Return `#t` if `object` is an object of type `<gdb:memory-port>`. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **memory-port-range** *memory-port*

:   Return the range of `<gdb:memory-port>` `memory-port` inclusive.

```
<!-- -->
```

Scheme Procedure: **memory-port-read-buffer-size** *memory-port*

:   Return the size of the read buffer of `<gdb:memory-port>` `memory-port`.

```
This procedure is deprecated and will be removed in [GDB] 11. It returns 0 when using Guile 2.2 or later.
```

```
<!-- -->
```

Scheme Procedure: **set-memory-port-read-buffer-size!** *memory-port size*

:   Set the size of the read buffer of `<gdb:memory-port>` `memory-port`. The result is unspecified.

```
This procedure is deprecated and will be removed in [GDB] is built with Guile 2.2 or later, you can call `setvbuf` instead (see [`setvbuf`](http://www.gnu.org/software/guile/manual/html_node/Buffering.html#Buffering) in GNU Guile Reference Manual).
```

```
<!-- -->
```

Scheme Procedure: **memory-port-write-buffer-size** *memory-port*

:   Return the size of the write buffer of `<gdb:memory-port>` `memory-port`.

```
This procedure is deprecated and will be removed in [GDB] is built with Guile 2.2 or later.
```

```
<!-- -->
```

Scheme Procedure: **set-memory-port-write-buffer-size!** *memory-port size*

:   Set the size of the write buffer of `<gdb:memory-port>` `memory-port`. The result is unspecified.

```
This procedure is deprecated and will be removed in [GDB] is built with Guile 2.2 or later, you can call `setvbuf` instead.
```

A memory port is closed like any other port, with `close-port`.

Combined with Guile's `bytevectors`, memory ports provide a lot of utility. For example, to fill a buffer of 10 integers in memory, one can do something like the following.

::: smallexample

```bash
;; In the program: int buffer[10];
(use-modules (rnrs bytevectors))
(use-modules (rnrs io ports))
(define addr (parse-and-eval "buffer"))
(define n 10)
(define byte-size (* n 4))
(define mem-port (open-memory #:mode "r+" #:start
                              (value->integer addr) #:size byte-size))
(define byte-vec (make-bytevector byte-size))
(do ((i 0 (+ i 1)))
    ((>= i n))
    (bytevector-s32-native-set! byte-vec (* i 4) (* i 42)))
(put-bytevector mem-port byte-vec)
(close-port mem-port)
```

:::

---

::: header
Next: [Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile)]
:::
