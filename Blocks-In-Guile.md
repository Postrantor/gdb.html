---
description: Blocks In Guile (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Blocks In Guile (Debugging with GDB)
lang: en
resource-type: document
title: Blocks In Guile (Debugging with GDB)
---
::: header
Next: [Symbols In Guile](Symbols-In-Guile.html#Symbols-In-Guile)]
:::

---

#### 23.4.3.16 Accessing blocks from Guile.

In [GDB], symbols are stored in blocks. A block corresponds roughly to a scope in the source code. Blocks are organized hierarchically, and are represented individually in Guile as an object of type `<gdb:block>`. Blocks rely on debugging information being available.

A frame has a block. Please see [Frames In Guile](Frames-In-Guile.html#Frames-In-Guile), for a more in-depth discussion of frames.

The outermost block is known as the *global block*. The global block typically holds public global variables and functions.

The block nested just inside the global block is the *static block*. The static block typically holds file-scoped variables and functions.

[GDB] provides a method to get a block's superblock, but there is currently no way to examine the sub-blocks of a block, or to iterate over all the blocks in a symbol table (see [Symbol Tables In Guile](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)).

Here is a short example that should help explain blocks:

::: smallexample

```bash
/* This is in the global block.  */
int global;

/* This is in the static block.  */
static int file_scope;

/* 'function' is in the global block, and 'argument' is
   in a block nested inside of 'function'.  */
int function (int argument)
{
  /* 'local' is in a block inside 'function'.  It may or may
     not be in the same block as 'argument'.  */
  int local;

  {
     /* 'inner' is in a block whose superblock is the one holding
        'local'.  */
     int inner;

     /* If this call is expanded by the compiler, you may see
        a nested block here whose function is 'inline_function'
        and whose superblock is the one holding 'inner'.  */
     inline_function ();
  }
}
```

:::

The following block-related procedures are provided by the `(gdb)` module:

Scheme Procedure: **block?** *object*

:   Return `#t` if `object` is a `<gdb:block>` object. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **block-valid?** *block*

:   Returns `#t` if `<gdb:block>` `block` is valid, `#f` if not. A block object can become invalid if the block it refers to doesn't exist anymore in the inferior. All other `<gdb:block>` methods will throw an exception if it is invalid at the time the procedure is called. The block's validity is also checked during iteration over symbols of the block.

```
<!-- -->
```

Scheme Procedure: **block-start** *block*

:   Return the start address of `<gdb:block>` `block`.

```
<!-- -->
```

Scheme Procedure: **block-end** *block*

:   Return the end address of `<gdb:block>` `block`.

```
<!-- -->
```

Scheme Procedure: **block-function** *block*

:   Return the name of `<gdb:block>` `block` represented as a `<gdb:symbol>` object. If the block is not named, then `#f` is returned.

```
For ordinary function blocks, the superblock is the static block. However, you should note that it is possible for a function block to have a superblock that is not the static block -- for instance this happens for an inlined function.
```

```
<!-- -->
```

Scheme Procedure: **block-superblock** *block*

:   Return the block containing `<gdb:block>` `block`. If the parent block does not exist, then `#f` is returned.

```
<!-- -->
```

Scheme Procedure: **block-global-block** *block*

:   Return the global block associated with `<gdb:block>` `block`.

```
<!-- -->
```

Scheme Procedure: **block-static-block** *block*

:   Return the static block associated with `<gdb:block>` `block`.

```
<!-- -->
```

Scheme Procedure: **block-global?** *block*

:   Return `#t` if `<gdb:block>` `block` is a global block. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **block-static?** *block*

:   Return `#t` if `<gdb:block>` `block` is a static block. Otherwise return `#f`.

```
<!-- -->
```

Scheme Procedure: **block-symbols**

:   Return a list of all symbols (as \<gdb:symbol\> objects) in `<gdb:block>` `block`.

```
<!-- -->
```

Scheme Procedure: **make-block-symbols-iterator** *block*

:   Return an object of type `<gdb:iterator>` that will iterate over all symbols of the block. Guile programs should not assume that a specific block object will always contain a given symbol, since changes in [GDB] features and infrastructure may cause symbols move across blocks in a symbol table. See [Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile).

```
<!-- -->
```

Scheme Procedure: **block-symbols-progress?**

:   Return #t if the object is a \<gdb:block-symbols-progress\> object. This object would be obtained from the `progress` element of the `<gdb:iterator>` object returned by `make-block-symbols-iterator`.

```
<!-- -->
```

Scheme Procedure: **lookup-block** *pc*

:   Return the innermost `<gdb:block>` containing the given `pc` value specified, the function will return `#f`.

---

::: header
Next: [Symbols In Guile](Symbols-In-Guile.html#Symbols-In-Guile)]
:::
